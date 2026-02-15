# FloatTranslate

실시간 영어→한국어 플로팅 번역 Android 애플리케이션

## 📱 개요

FloatTranslate는 플로팅 버블 UI를 통해 화면 위에서 실시간으로 음성을 인식하고 영어에서 한국어로 번역하는 Android 앱입니다.

### 주요 기능

- **플로팅 버블**: 화면 위에 항상 표시되는 번역 버튼
- **음성 인식**: 마이크를 통한 실시간 음성 입력 (Whisper)
- **실시간 번역**: 영어 → 한국어 번역 결과 표시
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
| ONNX Runtime | ML 모델 추론 (준비됨) |

## 📋 요구사항

- Android 8.0 (API 26) 이상
- 마이크 권한
- 오버레이 권한 (다른 앱 위에 표시)

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
- 실제 Whisper/번역 모델 통합 예정
