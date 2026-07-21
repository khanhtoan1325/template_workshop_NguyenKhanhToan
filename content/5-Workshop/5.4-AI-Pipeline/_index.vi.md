---
title: "AI/ML Pipeline"
date: 2026-07-17
weight: 4
chapter: false
pre: " <b> 5.4. </b> "
---

# Workshop 5.4: AI/ML Pipeline

---

## Mục tiêu học tập

Sau khi hoàn thành module này, bạn sẽ:

- Hiểu subtitle extraction sử dụng PaddleOCR
- Implement Speech-to-Text với Google Cloud
- Configure translation với Google Gemini API
- Generate voice-over với gTTS và ElevenLabs
- Handle video format validation và transcoding
- Implement error handling và retry mechanisms

---

## Điều kiện tiên quyết

- Hoàn thành Workshops 5.1-5.3
- Understanding của OCR concepts
- Basic knowledge của video codecs
- API keys đã configured

---

## Kiến trúc Pipeline


{{< image
  src="images/5-Workshop/5.4-AI-Pipeline/Pipeline AI - ML - v2.png"
  alt="Loi"
>}}

```
┌─────────────────────────────────────────────────────────────────────┐
│                        PROCESSING PIPELINE                          │
├─────────────────────────────────────────────────────────────────────┤
│  Video Input → Validation → OCR/STT → Translation → TTS → Render  │
└─────────────────────────────────────────────────────────────────────┘
```

---

## Step 1: Video Format Validation

### FFprobe Analysis

```python
# app/utils/video_validator.py
def analyze_video(video_path: str) -> Dict:
    """
    Analyze video file using FFprobe.
    """
    cmd = [
        'ffprobe', '-v', 'quiet',
        '-print_format', 'json',
        '-show_format', '-show_streams',
        video_path
    ]
    result = subprocess.run(cmd, capture_output=True, text=True)
    return json.loads(result.stdout)
```

### Format Compatibility Check

```python
def is_format_compatible(analysis: Dict) -> Tuple[bool, str]:
    """Check if video format is compatible."""
    video_codec = analysis.get('video_codec', '').lower()
    
    if 'h264' in video_codec or 'avc' in video_codec:
        return True, "H.264/AAC MP4 - fully compatible"
    
    if 'hevc' in video_codec or 'h265' in video_codec:
        return False, "HEVC/H.265 not supported, needs transcoding"
    
    return False, f"Unknown codec: {video_codec}"
```

---

## Step 2: OCR Subtitle Extraction

### PaddleOCR Configuration

```python
# app/modules/video_process.py
_ocr_instances_cache = {}
_default_lang = 'latin'

def get_ocr_instance(
    lang: str = None,
    det_db_thresh: float = 0.2,
    det_db_box_thresh: float = 0.5,
    use_angle_cls: bool = False,
    use_gpu: bool = False
):
    """Get or create OCR instance for the specified language."""
    global _ocr_instances_cache
    
    if lang is None:
        lang = _default_lang
    
    lang_map = {
        'en': 'latin', 'vi': 'latin',
        'zh': 'ch', 'ja': 'japan', 'ko': 'korean'
    }
    lang = lang_map.get(lang, lang)
    
    cache_key = f"{lang}_{det_db_thresh}_{det_db_box_thresh}"
    
    if cache_key not in _ocr_instances_cache:
        _ocr_instances_cache[cache_key] = PaddleOCR(
            use_angle_cls=use_angle_cls,
            lang=lang,
            det_db_thresh=det_db_thresh,
            det_db_box_thresh=det_db_box_thresh,
            use_gpu=use_gpu,
            show_log=False
        )
    
    return _ocr_instances_cache[cache_key]
```

### Video Frame Extraction

```python
def extract_subtitles_from_video(
    video_path: str,
    target_lang: str = None,
    fps_sample_rate: float = 1.0
) -> str:
    """Extract subtitles from video frames using OCR."""
    import cv2
    
    cap = cv2.VideoCapture(video_path)
    fps = cap.get(cv2.CAP_PROP_FPS)
    frame_interval = int(fps * fps_sample_rate)
    
    ocr = get_ocr_instance(lang=target_lang or 'latin')
    subtitles = []
    
    while cap.isOpened():
        ret, frame = cap.read()
        if not ret:
            break
        
        frame_count = cap.get(cv2.CAP_PROP_POS_FRAMES)
        
        if frame_count % frame_interval != 0:
            continue
        
        result = ocr.ocr(frame, cls=False)
        
        if result and result[0]:
            texts = [
                line[1][0] 
                for line in result[0] 
                if line[1][1] > 0.5 and len(line[1][0].strip()) > 2
            ]
            if texts:
                subtitles.append({
                    'start': cap.get(cv2.CAP_PROP_POS_MSEC) / 1000.0,
                    'end': cap.get(cv2.CAP_PROP_POS_MSEC) / 1000.0 + 2.0,
                    'text': ' '.join(texts)
                })
    
    cap.release()
    return subtitles_to_srt(subtitles)
```

### OCR Process Flow



{{< image
  src="images/5-Workshop/5.4-AI-Pipeline/OCR-v2.png"
  alt="Loi"
>}}
---

## Step 3: Speech-to-Text

### Google Cloud STT Integration

```python
# app/modules/module/module_speech_to_text.py
from google.cloud import speech_v1

def process_audio_to_subtitles(
    video_path: str,
    target_language: str = 'vi-VN'
) -> str:
    """Extract subtitles using Google Cloud Speech-to-Text."""
    
    # Extract audio from video
    audio_path = extract_audio_from_video(video_path)
    
    client = speech_v1.SpeechClient()
    
    with open(audio_path, 'rb') as f:
        content = f.read()
    
    audio = speech_v1.RecognitionAudio(content=content)
    
    config = speech_v1.RecognitionConfig(
        encoding=enums.RecognitionConfig.AudioEncoding.LINEAR16,
        sample_rate_hertz=16000,
        language_code=target_language,
        enable_automatic_punctuation=True,
        model='latest_long'
    )
    
    operation = client.long_running_recognize(config=config, audio=audio)
    response = operation.result(timeout=600)
    
    return convert_to_srt(response.results)
```

---

## Step 4: Translation with Gemini API

```python
# app/modules/video_process.py
import google.generativeai as genai

genai.configure(api_key=os.getenv('API_KEY'))
model = genai.GenerativeModel(os.getenv('API_MODEL', 'gemini-2.0-flash'))

def translate_srt(
    srt_content: str,
    target_language: str = 'vi'
) -> str:
    """Translate SRT content using Google Gemini API."""
    import pysrt
    
    subs = pysrt.open(io.StringIO(srt_content))
    translated_subs = []
    
    # Translate in batches
    batch_size = 10
    for i in range(0, len(subs), batch_size):
        batch = subs[i:i + batch_size]
        
        prompt = f"""Translate to {target_language}. Keep SRT format:
{chr(10).join([f"{sub.index}: {sub.text}" for sub in batch])}
Translation:"""
        
        try:
            response = model.generate_content(prompt)
            translated_batch = parse_translated_srt(response.text, batch)
            translated_subs.extend(translated_batch)
        except Exception as e:
            print(f"Translation error: {e}")
            translated_subs.extend(batch)
    
    output = pysrt.SubtitleFile(items=translated_subs)
    return str(output)
```

---

## Step 5: Text-to-Speech

### TTS Module

```python
# app/modules/module/module_text_to_speech_v4_parallel.py
def generate_audio_from_srt(
    srt_content: str,
    output_path: str,
    provider: str = 'gtts',
    voice_id: str = None
) -> str:
    """Generate TTS audio from SRT content."""
    import pysrt
    
    subs = pysrt.open(io.StringIO(srt_content))
    audio_segments = []
    
    for sub in subs:
        segment_audio = generate_segment_audio(
            text=sub.text,
            provider=provider,
            voice_id=voice_id
        )
        audio_segments.append({
            'audio': segment_audio,
            'start': sub.start.ordinal,
            'end': sub.end.ordinal
        })
    
    final_audio = concatenate_audio_segments(audio_segments)
    final_audio.export(output_path, format='mp3')
    
    return output_path
```

### Complete Data Flow



{{< image
  src="images/5-Workshop/5.4-AI-Pipeline/Data_flow.png"
  alt="Loi"
>}}
---

## Step 6: Video Rendering

```python
# app/modules/module/module_meger_video_v2.py
def process_video_with_sync(
    video_path: str,
    srt_path: str,
    audio_path: str = None,
    output_path: str = None
) -> str:
    """Merge video with subtitles and optional audio."""
    
    if audio_path:
        cmd = [
            'ffmpeg', '-i', video_path, '-i', audio_path,
            '-vf', f"subtitles='{srt_path}'",
            '-map', '0:v', '-map', '1:a',
            '-c:v', 'libx264', '-c:a', 'aac',
            '-shortest', '-y', output_path
        ]
    else:
        cmd = [
            'ffmpeg', '-i', video_path,
            '-vf', f"subtitles='{srt_path}'",
            '-c:v', 'libx264', '-c:a', 'copy',
            '-y', output_path
        ]
    
    subprocess.run(cmd, capture_output=True)
    return output_path
```

---

## Step 7: Error Handling

```python
# app/utils/provider_failure.py
def exponential_backoff(
    max_retries: int = 3,
    base_delay: float = 1.0,
    max_delay: float = 60.0
):
    """Decorator for exponential backoff retry."""
    def decorator(func):
        @wraps(func)
        def wrapper(*args, **kwargs):
            for attempt in range(max_retries):
                try:
                    return func(*args, **kwargs)
                except Exception as e:
                    delay = min(base_delay * (2 ** attempt), max_delay)
                    print(f"Retry {attempt + 1} in {delay}s: {e}")
                    time.sleep(delay)
            raise last_exception
        return wrapper
    return decorator
```

---

## Code References

| Component | File |
|-----------|------|
| Video Validation | `app/utils/video_validator.py` |
| OCR Engine | `app/modules/video_process.py` |
| STT Module | `app/modules/module/module_speech_to_text.py` |
| Translation | `app/modules/video_process.py` |
| TTS Module | `app/modules/module/module_text_to_speech_v4_parallel.py` |
| Video Render | `app/modules/module/module_meger_video_v2.py` |

---

## Tóm tắt

Trong module này, bạn đã học:

- **Video Validation**: FFprobe analysis và FFmpeg transcoding
- **OCR Extraction**: PaddleOCR với singleton pattern
- **Speech-to-Text**: Google Cloud STT cho audio transcription
- **Translation**: Gemini API với batch processing
- **Text-to-Speech**: gTTS và ElevenLabs integration
- **Video Rendering**: FFmpeg subtitle và audio composition
- **Error Handling**: Exponential backoff retry mechanism

---
