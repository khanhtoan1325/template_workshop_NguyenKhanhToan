---
title: "Video Localization Platform"
date: 2026-07-17
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

# Workshop 5.1: Video Localization Platform

---

## Learning Objectives

By the end of this module, you will:

- Understand the business problem this platform solves
- Comprehend the end-to-end video localization workflow
- Identify all AWS services and third-party integrations
- Read and interpret the system architecture diagram
- Understand the data flow between components

---

## Prerequisites

- Basic understanding of cloud computing concepts
- Familiarity with REST APIs
- Basic knowledge of video formats and codecs
- Understanding of database concepts

---

## Architecture Context

### The Business Problem

Video content localization traditionally requires multiple manual steps:

1. **Subtitle Extraction**: Extracting text from video frames using OCR software
2. **Translation**: Converting text from source to target language
3. **Timing Synchronization**: Aligning translated text with video timestamps
4. **Voice Recording**: Recording or generating voice-over audio
5. **Final Rendering**: Merging all elements into a complete localized video

This manual process is time-consuming, error-prone, and does not scale when handling multiple videos.

### The Solution

The Video Localization Platform automates this workflow through a cloud-native architecture that handles video upload through final render. The system uses:

- **PaddleOCR** for optical character recognition from video frames
- **Google Cloud Speech-to-Text** as an alternative for audio-based subtitle extraction
- **Google Gemini API** for context-aware translation
- **gTTS/ElevenLabs** for voice synthesis
- **FFmpeg** for video transcoding and rendering

---

## System Architecture

### High-Level Architecture Diagram

![System Architecture Overview](/images/5-Workshop/5.1-Workshop-overview/Kien-truc-he-thong-tong-quan.png)

### Component Overview

| Layer | Component | Technology | Purpose |
|-------|-----------|------------|---------|
| **Frontend** | Web Application | React 18, TypeScript, Vite | User interface for upload, editing, preview |
| **Frontend** | State Management | Zustand | Client-side state with persistence |
| **Frontend** | Real-time Updates | WebSocket | Live progress tracking |
| **Backend** | API Gateway | FastAPI | REST endpoints, authentication |
| **Backend** | Task Queue | Celery + Redis | Asynchronous processing |
| **Backend** | Database | MySQL (RDS) | Video metadata, user data |
| **Storage** | Object Storage | Amazon S3 | Video files, subtitles |
| **Storage** | Cache/Pub-Sub | Redis | Message broker, real-time events |
| **Processing** | OCR Engine | PaddleOCR | Text extraction from frames |
| **Processing** | Speech-to-Text | Google Cloud STT | Audio transcription |
| **Processing** | Translation | Google Gemini | Text translation |
| **Processing** | TTS | gTTS, ElevenLabs | Voice synthesis |
| **Processing** | Video Processing | FFmpeg, MoviePy | Transcoding, rendering |
| **Notification** | Email Service | Amazon SES | Completion notifications |

---

## Processing Pipeline

### Two-Stage Architecture

The platform uses a two-stage pipeline design that separates resource-intensive processing from user interaction:

![Two-Stage Pipeline](/images/5-Workshop/5.1-Workshop-overview/Luong-pipeline-2-giai-doan.png)

#### Stage 1: Extraction and Translation

```
Video Upload → Format Validation → OCR/STT Detection → Subtitle Extraction → Translation → SRT Upload
```

**Steps:**
1. User uploads video to S3
2. System validates video format using FFprobe
3. If format incompatible (HEVC, ProRes), auto-transcode to H.264/AAC
4. Detect whether to use OCR (embedded subtitles) or STT (audio only)
5. Extract subtitles using selected method
6. Translate subtitles using Gemini API
7. Upload translated SRT to S3
8. Send email notification via SES

**Status Transition:**
```
PROCESSING → AWAITING_REVIEW
```

#### Stage 2: Rendering and Final Output

```
User Edits → Approval → TTS Generation → Video Merge → Final Render → Download
```

**Steps:**
1. User reviews and edits subtitles in browser
2. User selects voice for dubbing (optional)
3. User clicks "Approve" to trigger Stage 2
4. Generate TTS audio from translated text
5. Merge video with subtitles and/or audio
6. Upload final video to S3
7. Send completion email

**Status Transition:**
```
AWAITING_REVIEW → STAGE2_PROCESSING → COMPLETED
```

---

## AWS Services Deep Dive

### Amazon S3

The platform uses three separate S3 buckets for logical data separation:

| Bucket | Purpose | Content Type |
|--------|---------|--------------|
| `ocr-video-bucket-*` | Input videos | Original uploads |
| `video-sub-ft-*` | Output videos | Final rendered videos |
| `srt-input-storage-*` | Subtitle files | SRT files (source + translated) |

**Security:** All bucket access uses presigned URLs with expiration to prevent unauthorized access.

### Amazon RDS MySQL

The database stores:

- **Video records**: Metadata, status, processing percentage, file URLs
- **SRT records**: Subtitle file references, language pairs
- **VIDEO_TTS records**: Final output tracking, voice generation details
- **User records**: Authentication and authorization

**Key fields:**
- `video_id`: Unique identifier (UUID)
- `status`: Current processing state
- `processing_percentage`: Real-time progress
- `file_url`, `video_url`, `video_tts_url`: S3 URL references

### Amazon SES

Email notifications sent at two points:

1. **Stage 1 completion**: Notifies user to review subtitles
2. **Stage 2 completion**: Notifies user video is ready for download

**Email content includes:**
- Video name
- Completion timestamp
- Status
- Download link (presigned URL)

### Redis

Dual role in the architecture:

1. **Message Broker**: Celery workers pull tasks from Redis queue
2. **Pub/Sub**: Real-time progress events broadcast to WebSocket clients

**Channels:**
- `progress:{video_id}`: Individual video progress updates
- `status:{video_id}`: Status change notifications

---

## Third-Party Service Integrations

### PaddleOCR

**Purpose:** Extract text from video frames (subtitles)

**Configuration:**
- Singleton pattern with model caching
- Language support: Chinese, Latin, Korean, Japanese, Arabic
- Default: Latin (English, Vietnamese)
- Optimized for 1 FPS sampling rate

**Code reference:**
```python
from app.modules.video_process import get_ocr_instance
ocr = get_ocr_instance(lang='latin')
```

### Google Cloud Speech-to-Text

**Purpose:** Transcribe audio when no embedded subtitles exist

**Use case:** Videos without hard-coded subtitles but with clear audio

**API:** `process_audio_to_subtitles()` in `module_speech_to_text.py`

### Google Gemini API

**Purpose:** Context-aware translation

**Model:** `gemini-2.0-flash` (configurable)

**Features:**
- Automatic language detection
- Batch processing for efficiency
- Retry with exponential backoff

**Code reference:**
```python
from app.modules.video_process import translate_srt
translated_content = translate_srt(srt_content, target_lang='vi')
```

### gTTS and ElevenLabs

**Purpose:** Text-to-Speech for dubbing

| Provider | Quality | Cost | Use Case |
|----------|---------|------|----------|
| gTTS | Standard | Free | Default option |
| ElevenLabs | Natural | Paid | Premium voices |

**Code reference:**
```python
from app.modules.module.module_text_to_speech_v4_parallel import generate_audio_from_srt
```

---

## Real-Time Progress Tracking

### WebSocket Architecture

```
┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│   Browser    │────▶│   FastAPI    │◀────│    Redis     │
│   (React)    │◀────│   Backend   │────▶│   Pub/Sub    │
└──────────────┘     └──────────────┘     └──────────────┘
       ▲                    │                    ▲
       │                    │                    │
       └────────────────────┴────────────────────┘
                    WebSocket
```

### Progress Data Structure

```typescript
interface ProgressData {
  video_id: string;
  percentage: number;    // 0-100
  status: VideoStatus;  // PROCESSING | AWAITING_REVIEW | etc.
  message: string;      // Human-readable status
  stage?: string;       // STAGE1_INIT | STAGE1_DOWNLOAD | etc.
  error_code?: string;   // For error states
}
```

### Frontend Integration

```typescript
// From useVideoProgress.ts
const ws = new WebSocket(`${WS_URL}/progress/${videoId}`);
ws.onmessage = (event) => {
  const progress: ProgressData = JSON.parse(event.data);
  updateProgress(progress);
};
```

---

## Video Format Handling

### Validation with FFprobe

Before processing, all videos are validated:

```python
from app.utils.video_validator import analyze_video, is_format_compatible

analysis = analyze_video(video_path)
is_compatible, reason = is_format_compatible(analysis)
```

### Supported Formats

| Status | Formats | Handling |
|--------|---------|----------|
| **Compatible** | MP4, MOV (H.264 + AAC) | Fast copy with optimization |
| **Requires Transcode** | HEVC, ProRes, VP9 | FFmpeg to H.264/AAC |
| **Unsupported** | Others | Error with guidance |

### Auto-Transcode Logic

```python
if not is_actually_compatible:
    transcode_to_mp4_h264(input_path, output_path, force_transcode=True)
```

---

## Security Considerations

### Authentication

- JWT tokens for API authentication
- Token expiration and refresh
- WebSocket authentication via query parameters

### Authorization

- User can only access their own videos
- S3 access via presigned URLs (time-limited)

### Data Protection

- Database credentials in environment variables
- API keys managed via AWS Secrets Manager (recommended)
- No sensitive data in logs

---

## Summary

In this module, you learned:

- **Business Context**: Why automated video localization solves real problems
- **Architecture Overview**: The two-stage pipeline design
- **AWS Services**: S3, RDS, SES, and their roles
- **Third-Party Integrations**: OCR, STT, Translation, TTS
- **Real-Time Updates**: WebSocket and Redis Pub/Sub
- **Video Processing**: FFprobe validation and FFmpeg transcoding

---

## References

- [FastAPI Documentation](https://fastapi.tiangolo.com/)
- [Celery Documentation](https://docs.celeryproject.org/)
- [PaddleOCR](https://github.com/PaddlePaddle/PaddleOCR)
- [Google Gemini API](https://ai.google.dev/)
- [FFmpeg Documentation](https://ffmpeg.org/documentation.html)

