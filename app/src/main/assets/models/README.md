# Whisper ONNX Models

This directory contains the Whisper Tiny ONNX models for on-device speech recognition.

## Model Files

The following models are automatically downloaded during the GitHub Actions build process:

1. **encoder_model_quantized.onnx**
   - Source: `onnx-community/whisper-tiny` on Hugging Face
   - URL: https://huggingface.co/onnx-community/whisper-tiny/resolve/main/onnx/encoder_model_quantized.onnx
   - Purpose: Audio feature extraction from mel-spectrograms
   - Size: ~24 MB (quantized INT8)

2. **decoder_model_quantized.onnx**
   - Source: `onnx-community/whisper-tiny` on Hugging Face
   - URL: https://huggingface.co/onnx-community/whisper-tiny/resolve/main/onnx/decoder_model_quantized.onnx
   - Purpose: Token generation for transcription
   - Size: ~24 MB (quantized INT8)

## Model Details

- **Model**: Whisper Tiny (OpenAI)
- **Format**: ONNX (optimized for mobile)
- **Quantization**: INT8 (for reduced size and faster inference)
- **Language**: English
- **Use Case**: On-device speech recognition for Android

## Manual Download

If you need to manually download the models for local development:

```bash
mkdir -p app/src/main/assets/models
cd app/src/main/assets/models

# Download encoder model
curl -fL "https://huggingface.co/onnx-community/whisper-tiny/resolve/main/onnx/encoder_model_quantized.onnx" \
  -o encoder_model_quantized.onnx

# Download decoder model
curl -fL "https://huggingface.co/onnx-community/whisper-tiny/resolve/main/onnx/decoder_model_quantized.onnx" \
  -o decoder_model_quantized.onnx
```

## Integration

The models are loaded and used by `WhisperEngine.kt` for real-time speech recognition.
Currently, the app uses a mock implementation, but the models are ready for integration.

## License

The Whisper models are provided by OpenAI and distributed through the ONNX Community on Hugging Face.
See the original repository for license information:
https://huggingface.co/onnx-community/whisper-tiny
