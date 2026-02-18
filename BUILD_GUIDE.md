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

# (권장) Java 17 고정 (.tool-versions 사용)
mise install
mise exec -- java -version

# 또는 직접 JAVA_HOME 지정
# export JAVA_HOME=~/.local/share/mise/installs/java/17.0.2
# export PATH="$JAVA_HOME/bin:$PATH"

# Android SDK 경로 지정 (최초 1회)
# local.properties 파일 생성
echo "sdk.dir=$HOME/android-sdk" > local.properties

# cmdline-tools 설치 후 SDK 패키지 설치
# yes | sdkmanager --licenses
# sdkmanager "platform-tools" "platforms;android-34" "build-tools;34.0.0"

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
- Voxtral GGUF 모델 실제 추론 엔진 연동 (현재 Mock)
- 번역 모델(Gemma 등) 모바일 추론 파이프라인 연동

---

## 모델 다운로드

GitHub Actions 기본 빌드는 APK 생성 안정성을 위해 모델 대용량 파일을 다운로드하지 않습니다.

`workflow_dispatch`에서 `include_model=true`로 실행하면 모델 메타데이터만 내려받아 검증할 수 있습니다.

실제 모델 파일은 수동으로 다운로드하세요:
```bash
cd app/src/main/assets/models
curl -fL "https://huggingface.co/TrevorJS/voxtral-mini-realtime-gguf/resolve/main/voxtral-q4.gguf" -o voxtral-q4.gguf
```

자세한 내용은 `app/src/main/assets/models/README.md` 참조

---

## 빠른 시작

프로젝트를 ZIP으로 다운로드하세요:
```powershell
# PowerShell에서
Compress-Archive -Path FloatTranslate -DestinationPath FloatTranslate.zip
```

그리고 Android Studio에서 열기만 하면 됩니다!
