---
title: "Video Localization Platform"
date: 2026-07-17
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

# Workshop 5.1: Video Localization Platform

---

## Mục tiêu học tập

Sau khi hoàn thành module này, bạn sẽ:

- Hiểu bài toán kinh doanh mà nền tảng này giải quyết
- Nắm vững workflow dịch thuật và lồng tiếng video end-to-end
- Xác định tất cả các dịch vụ AWS và tích hợp bên thứ ba
- Đọc và diễn giải sơ đồ kiến trúc hệ thống
- Hiểu luồng dữ liệu giữa các thành phần

---

## Điều kiện tiên quyết

- Hiểu biết cơ bản về cloud computing
- Quen thuộc với REST APIs
- Kiến thức cơ bản về định dạng và codec video
- Hiểu về khái niệm database

---

## Kiến trúc hệ thống

### Sơ đồ Kiến trúc Tổng quan

![Kiến trúc hệ thống tổng quan](/images/5-Workshop/5.1-Workshop-overview/Kien-truc-he-thong-tong-quan.png)

### Tổng quan các thành phần

| Layer | Component | Technology | Purpose |
|-------|-----------|------------|---------|
| **Frontend** | Web Application | React 18, TypeScript, Vite | Giao diện người dùng cho upload, chỉnh sửa, xem trước |
| **Frontend** | State Management | Zustand | Trạng thái phía client với persistence |
| **Frontend** | Real-time Updates | WebSocket | Theo dõi tiến độ trực tiếp |
| **Backend** | API Gateway | FastAPI | REST endpoints, xác thực |
| **Backend** | Task Queue | Celery + Redis | Xử lý bất đồng bộ |
| **Backend** | Database | MySQL (RDS) | Video metadata, user data |
| **Storage** | Object Storage | Amazon S3 | Video files, subtitles |
| **Storage** | Cache/Pub-Sub | Redis | Message broker, real-time events |
| **Processing** | OCR Engine | PaddleOCR | Trích xuất text từ frames |
| **Processing** | Speech-to-Text | Google Cloud STT | Audio transcription |
| **Processing** | Translation | Google Gemini | Dịch thuật text |
| **Processing** | TTS | gTTS, ElevenLabs | Tổng hợp giọng nói |
| **Processing** | Video Processing | FFmpeg, MoviePy | Transcoding, rendering |
| **Notification** | Email Service | Amazon SES | Thông báo hoàn thành |

---

## Processing Pipeline

### Kiến trúc hai giai đoạn

Nền tảng sử dụng thiết kế pipeline hai giai đoạn tách biệt xử lý tốn tài nguyên khỏi tương tác người dùng:

![Luồng pipeline 2 giai đoạn](/images/5-Workshop/5.1-Workshop-overview/Luong-pipeline-2-giai-doan.png)

#### Giai đoạn 1: Trích xuất và Dịch thuật

```
Video Upload → Format Validation → OCR/STT Detection → Subtitle Extraction → Translation → SRT Upload
```

**Các bước:**
1. Người dùng upload video lên S3
2. Hệ thống xác thực định dạng video sử dụng FFprobe
3. Nếu định dạng không tương thích (HEVC, ProRes), tự động transcode sang H.264/AAC
4. Phát hiện nên dùng OCR (phụ đề nhúng) hay STT (chỉ audio)
5. Trích xuất phụ đề sử dụng phương pháp được chọn
6. Dịch phụ đề sử dụng Gemini API
7. Upload SRT đã dịch lên S3
8. Gửi thông báo email qua SES

**Chuyển đổi trạng thái:**
```
PROCESSING → AWAITING_REVIEW
```

#### Giai đoạn 2: Rendering và Output cuối cùng

```
User Edits → Approval → TTS Generation → Video Merge → Final Render → Download
```

**Các bước:**
1. Người dùng xem lại và chỉnh sửa phụ đề trong trình duyệt
2. Người dùng chọn giọng cho dubbing (tùy chọn)
3. Người dùng click "Approve" để kích hoạt Giai đoạn 2
4. Tạo TTS audio từ text đã dịch
5. Ghép video với phụ đề và/hoặc audio
6. Upload video cuối cùng lên S3
7. Gửi thông báo hoàn thành

**Chuyển đổi trạng thái:**
```
AWAITING_REVIEW → STAGE2_PROCESSING → COMPLETED
```

---

## Chi tiết các dịch vụ AWS

### Amazon S3

Nền tảng sử dụng ba bucket S3 riêng biệt cho việc phân tách dữ liệu logic:

| Bucket | Mục đích | Loại nội dung |
|--------|-----------|--------------|
| `ocr-video-bucket-*` | Video đầu vào | Original uploads |
| `video-sub-ft-*` | Video đầu ra | Final rendered videos |
| `srt-input-storage-*` | File phụ đề | SRT files (source + translated) |

**Bảo mật:** Tất cả bucket access sử dụng presigned URLs với expiration để ngăn chặn truy cập trái phép.

### Amazon RDS MySQL

Database lưu trữ:

- **Video records**: Metadata, status, processing percentage, file URLs
- **SRT records**: Subtitle file references, language pairs
- **VIDEO_TTS records**: Final output tracking, voice generation details
- **User records**: Authentication và authorization

**Các trường quan trọng:**
- `video_id`: Unique identifier (UUID)
- `status`: Current processing state
- `processing_percentage`: Real-time progress
- `file_url`, `video_url`, `video_tts_url`: S3 URL references

### Amazon SES

Email notifications được gửi tại hai thời điểm:

1. **Stage 1 completion**: Thông báo cho user xem lại phụ đề
2. **Stage 2 completion**: Thông báo cho user video đã sẵn sàng tải về

**Email content bao gồm:**
- Video name
- Completion timestamp
- Status
- Download link (presigned URL)

### Redis

Vai trò kép trong kiến trúc:

1. **Message Broker**: Celery workers pull tasks từ Redis queue
2. **Pub/Sub**: Real-time progress events broadcast đến WebSocket clients

**Channels:**
- `progress:{video_id}`: Individual video progress updates
- `status:{video_id}`: Status change notifications

---

## Tích hợp dịch vụ bên thứ ba

### PaddleOCR

**Mục đích:** Trích xuất text từ video frames (phụ đề)

**Cấu hình:**
- Singleton pattern với model caching
- Hỗ trợ ngôn ngữ: Chinese, Latin, Korean, Japanese, Arabic
- Default: Latin (English, Vietnamese)
- Tối ưu cho tốc độ lấy mẫu 1 FPS

### Google Cloud Speech-to-Text

**Mục đích:** Phiên âm audio khi không có phụ đề nhúng

**Use case:** Videos không có phụ đề hard-coded nhưng có audio rõ ràng

### Google Gemini API

**Mục đích:** Dịch thuật nhận biết ngữ cảnh

**Model:** `gemini-2.0-flash` (có thể cấu hình)

**Tính năng:**
- Automatic language detection
- Batch processing cho hiệu quả
- Retry với exponential backoff

### gTTS và ElevenLabs

**Mục đích:** Text-to-Speech cho dubbing

| Provider | Chất lượng | Chi phí | Use Case |
|----------|-----------|---------|----------|
| gTTS | Standard | Miễn phí | Tùy chọn mặc định |
| ElevenLabs | Tự nhiên | Trả phí | Giọng premium |

---

## Theo dõi tiến độ Real-time

### Kiến trúc WebSocket

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

### Cấu trúc dữ liệu Progress

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

---

## Xử lý định dạng Video

### Validation với FFprobe

Trước khi xử lý, tất cả videos được xác thực:

```python
from app.utils.video_validator import analyze_video, is_format_compatible

analysis = analyze_video(video_path)
is_compatible, reason = is_format_compatible(analysis)
```

### Các định dạng được hỗ trợ

| Status | Formats | Xử lý |
|--------|---------|--------|
| **Tương thích** | MP4, MOV (H.264 + AAC) | Fast copy với optimization |
| **Cần Transcode** | HEVC, ProRes, VP9 | FFmpeg sang H.264/AAC |
| **Không hỗ trợ** | Others | Error với hướng dẫn |

---

## Bảo mật

### Xác thực

- JWT tokens cho API authentication
- Token expiration và refresh
- WebSocket authentication qua query parameters

### Ủy quyền

- User chỉ có thể truy cập videos của chính họ
- S3 access qua presigned URLs (time-limited)

### Bảo vệ dữ liệu

- Database credentials trong environment variables
- API keys quản lý qua AWS Secrets Manager (recommended)
- Không có sensitive data trong logs

---

## Tóm tắt

Trong module này, bạn đã học:

- **Bối cảnh kinh doanh**: Tại sao dịch thuật video tự động giải quyết vấn đề thực
- **Tổng quan kiến trúc**: Thiết kế pipeline hai giai đoạn
- **AWS Services**: S3, RDS, SES và vai trò của chúng
- **Tích hợp bên thứ ba**: OCR, STT, Translation, TTS
- **Real-time Updates**: WebSocket và Redis Pub/Sub
- **Xử lý Video**: FFprobe validation và FFmpeg transcoding

---

## Tham khảo

- [FastAPI Documentation](https://fastapi.tiangolo.com/)
- [Celery Documentation](https://docs.celeryproject.org/)
- [PaddleOCR](https://github.com/PaddlePaddle/PaddleOCR)
- [Google Gemini API](https://ai.google.dev/)
- [FFmpeg Documentation](https://ffmpeg.org/documentation.html)

