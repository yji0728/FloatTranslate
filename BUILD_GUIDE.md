# FloatTranslate 자동 빌드 가이드

## 방법 1: GitHub Actions (권장)

### 1. GitHub 레포지토리 생성
1. https://github.com/new 에서 새 레포지토리 생성
2. 이름: `FloatTranslate`
3. Public 또는 Private 선택

### 2. 프로젝트 푸시
```bash
cd FloatTranslate
git remote add origin https://github.com/YOUR_USERNAME/FloatTranslate.git
git push -u origin master
```

### 3. APK 다운로드
1. GitHub에서 Actions 탭 클릭
2. "Build APK" 워크플로우 클릭
3. 완료 후 Artifacts에서 APK 다운로드

---

## 방법 2: 직접 빌드 (WSL2)

이미 프로젝트가 준비되어 있습니다. Android SDK만 설치하면 됩니다.

```bash
# WSL2에서 실행
cd /mnt/c/Users/yjisec/.openclaw/workspace/FloatTranslate

# Gradle wrapper 다운로드
./gradlew --version

# 디버그 APK 빌드
./gradlew assembleDebug

# APK 위치
# app/build/outputs/apk/debug/app-debug.apk
```

---

## 방법 3: Android Studio (GUI)

1. Android Studio 다운로드: https://developer.android.com/studio
2. FloatTranslate 프로젝트 열기
3. Build → Build Bundle(s) / APK(s) → Build APK(s)

---

## 프로젝트 현재 상태

✅ **완료된 항목:**
- Kotlin 소스 코드 (MainActivity, FloatingWindowService, WhisperEngine)
- Jetpack Compose UI
- AndroidManifest.xml 및 리소스 파일
- build.gradle.kts 설정
- GitHub Actions workflow
- README.md 및 기술 문서

⏳ **남은 작업:**
- 실제 APK 빌드 (SDK 필요)
- Whisper ONNX 모델 통합
- Gemma GGUF 모델 통합

---

## 빠른 시작

프로젝트를 ZIP으로 다운로드하세요:
```powershell
# PowerShell에서
Compress-Archive -Path FloatTranslate -DestinationPath FloatTranslate.zip
```

그리고 Android Studio에서 열기만 하면 됩니다!
