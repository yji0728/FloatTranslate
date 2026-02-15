# FloatTranslate 프로젝트 명세서

## 1. 프로젝트 개요

**프로젝트명:** FloatTranslate  
**플랫폼:** Android  
**최소 SDK:** 26 (Android 8.0)  
**타겟 SDK:** 34 (Android 14)

플로팅 버블 UI를 통한 실시간 음성 인식 및 영어→한국어 번역 Android 애플리케이션

---

## 2. 주요 기능

### 2.1 핵심 기능

| 기능 | 설명 | 상태 |
|------|------|------|
| 플로팅 버블 | 화면 위에 항상 표시되는 번역 버튼 | ✅ 완료 |
| 음성 인식 | 마이크를 통한 실시간 음성 입력 | ✅ 완료 (Mock) |
| 실시간 번역 | 영어 → 한국어 번역 결과 표시 | ✅ 완료 (Mock) |
| Foreground Service | 백그라운드 번역 서비스 실행 | ✅ 완료 |

### 2.2 기술 스택

| 기술 | 용도 | 상태 |
|------|------|------|
| Jetpack Compose | UI 프레임워크 | ✅ 완료 |
| Kotlin Coroutines | 비동기 처리 | ✅ 완료 |
| WindowManager | 플로팅 창 구현 | ✅ 완료 |
| AudioRecord | 오디오 캡처 | ✅ 완료 |
| ONNX Runtime | Whisper 모델 추론 | ⚙️ 준비됨 |
| Material 3 | 디자인 시스템 | ✅ 완료 |

---

## 3. 구현 현황

### 3.1 완료된 항목

- [x] **프로젝트 구조** - Gradle, Kotlin, Compose 기반 Android 프로젝트
- [x] **MainActivity** - 권한 요청 및 서비스 시작/중지 UI
- [x] **FloatingWindowService** - 플로팅 버블 및 번역 카드 UI
- [x] **WhisperEngine** - 음성 인식 엔진 (Mock 구현)
- [x] **번역 UI** - 원문/번역문 표시 카드
- [x] **권한 처리** - 마이크, 오버레이, 알림 권한

### 3.2 待 구현 (차후 버전)

- [ ] **실제 Whisper 모델** - assets/models/whisper-tiny.onnx 파일 추가
- [ ] **실제 번역 모델** - Gemma 2B 또는 Llama 기반 번역
- [ ] **설정 화면** - 언어 선택, 모델 선택 등
- [ ] **번역 기록** - SharedPreferences 기반 저장

---

## 4. 빌드 의존성

```kotlin
// build.gradle.kts (app)
dependencies {
    // Core
    implementation("androidx.core:core-ktx:1.12.0")
    implementation("androidx.lifecycle:lifecycle-runtime-ktx:2.7.0")
    implementation("androidx.lifecycle:lifecycle-service:2.7.0")
    
    // Compose
    implementation("androidx.activity:activity-compose:1.8.2")
    implementation(platform("androidx.compose:compose-bom:2024.02.00"))
    implementation("androidx.compose.material3:material3")
    implementation("androidx.compose.material:material-icons-extended")
    
    // Coroutines
    implementation("org.jetbrains.kotlinx:kotlinx-coroutines-android:1.7.3")
    
    // ONNX Runtime (실제 모델 사용시)
    implementation("com.microsoft.onnxruntime:onnxruntime-mobile:1.16.3")
}
```

---

## 5. 아키텍처

```
com.floattranslate/
├── MainActivity.kt           # 메인 화면 (권한 요청, 서비스 제어)
├── FloatTranslateApp.kt      # Application 클래스
├── service/
│   └── FloatingWindowService.kt  # 플로팅 창 서비스
├── ml/
│   └── WhisperEngine.kt      # 음성 인식 엔진 (Mock)
└── ui/
    └── theme/
        ├── Theme.kt          # Compose 테마
        └── Type.kt           # 타이포그래피
```

---

## 6. 권한 목록

| 권한 | 용도 |
|------|------|
| RECORD_AUDIO | 음성 인식 |
| SYSTEM_ALERT_WINDOW | 플로팅 창 표시 |
| FOREGROUND_SERVICE | 백그라운드 서비스 |
| FOREGROUND_SERVICE_MICROPHONE | 마이크 사용 알림 |
| POST_NOTIFICATIONS | 알림 표시 |
| INTERNET | 번역 API 연동 (차후) |
| WAKE_LOCK | 화면 꺼짐 상태 유지 |

---

## 7. 버전 정보

- **v1.0.0** - MVP (Mock 기반)
- **v1.1.0** - 실제 Whisper/번역 모델 통합 (예정)
