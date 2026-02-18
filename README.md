# FloatTranslate

실시간 영어→한국어 플로팅 번역 Android 애플리케이션

## 📱 개요

FloatTranslate는 플로팅 버블 UI를 통해 화면 위에서 실시간으로 음성을 인식하고 영어에서 한국어로 번역하는 Android 앱입니다.

### 주요 기능

- **플로팅 버블**: 화면 위에 항상 표시되는 번역 버튼
- **음성 인식**: 마이크를 통한 실시간 음성 입력 (Voxtral GGUF 예정, 현재 Mock 엔진)
- **실시간 번역**: 영어 → 한국어 번역 결과 표시
- **권한 체크**: Android 설치 후 마이크/오버레이 권한 흐름 제공
- **백그라운드 지원**: Foreground Service로 백그라운드 번역

## 🛠 기술 스택

| 기술 | 설명 |
|------|------|
| Kotlin | 프로그래밍 언어 |
| Jetpack Compose | UI 프레임워크 |
| Material 3 | 디자인 시스템 |
| Coroutines | 비동기 처리 |
| WindowManager | 플로팅 창 구현 |
| AudioRecord | 오디오 캡처 |
| GGUF Runtime (llama.cpp 계열) | ML 모델 추론 (준비됨) |

## 📋 요구사항


- Android 8.0 (API 26) 이상
- 마이크 권한
- 오버레이 권한 (다른 앱 위에 표시)


## 🔐 오디오 권한 관련 중요 사항

- 이 앱은 `RECORD_AUDIO` 권한으로 **마이크 입력**을 받습니다.
- Android 일반 앱은 설치/런타임 권한만으로 **시스템 전체 오디오(다른 앱 소리)**를 직접 캡처할 수 없습니다.
- `CAPTURE_AUDIO_OUTPUT`은 시스템/시그니처 권한이라 일반 배포 앱에서는 사용 불가합니다.
- 시스템 오디오가 꼭 필요하면 `MediaProjection` 기반 사용자 동의 플로우(화면 캡처 + 오디오)를 별도 구현해야 합니다.

## 🤖 모델 비교 및 교체 결과

기존 선택 모델(Whisper Tiny ONNX)과 아래 모델을 비교했습니다.

- 비교 대상: https://huggingface.co/TrevorJS/voxtral-mini-realtime-gguf

### 비교 요약

| 항목 | Whisper Tiny ONNX | Voxtral Mini Realtime GGUF |
|------|-------------------|------------------------------|
| 포맷 | ONNX INT8 (encoder/decoder 분리) | GGUF Q4 (단일 파일) |
| 용량 | 약 24MB + 24MB | 약 2.51GB |
| 특성 | 매우 경량, 품질/문맥 한계 | Realtime ASR 특화, 성능 기대치 높음 |
| 모바일 적용 | APK 포함 용이 | 대용량 다운로드/캐싱 전략 필요 |

### 결정

- 정확도/실시간성 개선 목적에 맞춰 **Voxtral Mini Realtime GGUF로 교체**했습니다.
- 빌드 파이프라인은 APK 실제 빌드 성공을 우선하며, 대용량 모델(2.5GB)은 CI에서 기본 다운로드하지 않도록 조정했습니다.

## 📦 설치 방법

### 1. 저장소 클론

```bash
git clone https://github.com/your-repo/FloatTranslate.git
cd FloatTranslate
```

### 2. 빌드

```bash
./gradlew assembleDebug
```

### 3. APK 설치

```bash
adb install app/build/outputs/apk/debug/app-debug.apk
```

## 🚀 사용 방법

1. 앱을 실행합니다
2. 마이크 권한과 오버레이 권한을 허용합니다
3. "번역 시작" 버튼을 누릅니다
4. 화면에 나타나는 플로팅 버블을 눌러 번역 카드를 엽니다
5. 마이크 버튼을 누르고 영어로 말하면 한국어 번역이 표시됩니다

## 📂 프로젝트 구조

```
app/src/main/java/com/floattranslate/
├── MainActivity.kt           # 메인 화면
├── FloatTranslateApp.kt     # Application 클래스
├── service/
│   └── FloatingWindowService.kt  # 플로팅 창 서비스
├── ml/
│   └── WhisperEngine.kt      # 음성 인식 엔진
└── ui/
    └── theme/
        ├── Theme.kt          # Compose 테마
        └── Type.kt           # 타이포그래피
```

## ⚙️ 빌드 설정

```kotlin
// build.gradle.kts (app)
minSdk = 26
targetSdk = 34
compileSdk = 34
```

## 📄 라이선스

MIT License

## 📝 버전 정보

- **v1.0.0** - MVP (Mock 기반)
- **v1.1.0** - 실제 Voxtral/GGUF 모델 통합 (진행 중)
  - Voxtral Mini Realtime Q4 모델 다운로드 파이프라인 반영
  - GitHub Actions에서 자동 모델 다운로드
  - 준비 완료: APK 빌드에 모델 포함 (대용량 배포 전략 별도 필요)
