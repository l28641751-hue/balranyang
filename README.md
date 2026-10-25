# 발라냥

새끼 고양이가 모자이크 생선을 발라먹는 퍼즐 게임 (웹앱 / PWA).

<p align="center"><a href="https://l28641751-hue.github.io/balranyang/"><img src="https://img.shields.io/badge/%E2%96%B6%20%EB%B0%94%EB%A1%9C%20%ED%94%8C%EB%A0%88%EC%9D%B4-%EB%B0%9C%EB%9D%BC%EB%83%A5-ff7a2f?style=for-the-badge" alt="바로 플레이"></a></p>

<p align="center"><img src="web/qr.png" width="180" alt="QR 코드"><br>폰 카메라로 QR을 찍으면 바로 시작해요</p>

- 바로 플레이: https://l28641751-hue.github.io/balranyang/
- 친구에게 공유(QR·링크 복사·공유 버튼): https://l28641751-hue.github.io/balranyang/share.html

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
