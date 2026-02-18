# On-device ASR Models

This directory contains the speech recognition model used by FloatTranslate.

## Current Selected Model

1. **voxtral-q4.gguf**
   - Source: `TrevorJS/voxtral-mini-realtime-gguf` on Hugging Face
   - URL: https://huggingface.co/TrevorJS/voxtral-mini-realtime-gguf/resolve/main/voxtral-q4.gguf
   - Format: GGUF (Q4 quantized)
   - Pipeline tag: `automatic-speech-recognition`
   - Size: ~2.51 GB
   - Purpose: Realtime multilingual ASR for on-device/mobile-targeted runtime (llama.cpp/ggml 계열)

## Why this model replaced Whisper Tiny ONNX

- 기존 `onnx-community/whisper-tiny`는 경량(각 24MB 수준)이나 정확도/실시간성 측면에서 제한이 있었습니다.
- `voxtral-mini-realtime-gguf`는 음성 인식 특화 리얼타임 모델이며, 다국어 지원 범위가 더 넓고 최신 ASR 성능을 기대할 수 있습니다.
- 단, 모델 용량이 매우 크므로(약 2.5GB) Android 배포 전략(AAB 분리, 최초 실행 다운로드, 외부 저장소 캐싱) 검토가 필요합니다.

## Manual Download

If you need to manually download the model for local development:

```bash
mkdir -p app/src/main/assets/models
cd app/src/main/assets/models

curl -fL "https://huggingface.co/TrevorJS/voxtral-mini-realtime-gguf/resolve/main/voxtral-q4.gguf" \
  -o voxtral-q4.gguf
```


## CI Note

- GitHub Actions 기본 빌드에서는 APK 생성 시간을 위해 `voxtral-q4.gguf` 전체 파일을 받지 않습니다.
- 필요 시 워크플로 수동 실행(`workflow_dispatch`)에서 메타데이터 검증을 수행하고, 실제 모델은 배포/런타임 단계에서 별도 다운로드 전략을 권장합니다.

## Integration Note

`WhisperEngine.kt` is currently a mock wrapper and should be connected to a GGUF-capable inference runtime.

## License

See the model card for license and usage terms:
https://huggingface.co/TrevorJS/voxtral-mini-realtime-gguf
