# 발라냥

새끼 고양이가 모자이크 생선을 발라먹는 퍼즐 게임 (웹앱 / PWA).

플레이: https://l28641751-hue.github.io/balranyang/

- Android(Chrome): 메뉴(⋮) → 홈 화면에 추가 / 앱 설치
- iPhone(Safari): 공유 버튼 → 홈 화면에 추가

## 구조
- `web/` : 웹앱(PWA) — GitHub Pages로 배포, Capacitor 앱의 화면(webDir)
- `android/`, `ios/` : Capacitor 네이티브 프로젝트
- `store/` : 스토어 등록 문구, 스크린샷, 설문 답안, 출시 체크리스트 (`RELEASE_CHECKLIST.md` 먼저 읽기)
- `.github/workflows/` : Pages 배포, Android 빌드, iOS 컴파일 확인

## 앱 빌드
```
npm ci
npx cap sync
# Android: cd android && ./gradlew assembleDebug   (JDK 21 필요)
# iOS: npx cap open ios                              (Mac + Xcode 필요)
```
