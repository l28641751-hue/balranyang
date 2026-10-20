# 발라냥 스토어 출시 체크리스트

## 0. 지금 준비된 것 (이 저장소 안)
- [x] 안드로이드·iOS 앱 프로젝트 (Capacitor 8) — `android/`, `ios/`
- [x] 앱 아이콘·시작 화면(안드로이드 전 해상도, iOS) 자동 생성
- [x] 글꼴·그림 전부 앱 안에 포함 → 외부 서버 통신 없음(개인정보·오프라인 요건 충족)
- [x] 앱 버전에서는 결제 미리보기(가짜 결제 UI) 자동 숨김 — 애플 심사에서 "미완성 기능"으로 거절될 수 있는 부분
- [x] 진동(햅틱)을 네이티브로 연결 (아이폰은 웹 진동이 없어서)
- [x] 세로 화면 고정, 아이폰 전용(아이패드 제외)
- [x] 개인정보 처리방침 페이지 (`web/privacy.html`)
- [x] 스토어 문구(한/영), 스크린샷(Android 1080×1920, iPhone 6.9" 1320×2868 각 7장), 대표 그래픽, 512 아이콘
- [x] 자동 빌드: GitHub Actions가 안드로이드 APK/AAB, iOS 컴파일 확인을 수행

## 1. 먼저 정해야 할 것 (제가 대신 정할 수 없는 것)
1. **개발자 이름/회사명, 문의 이메일** → `web/privacy.html` 맨 아래 "문의 이메일" 칸과 스토어 저작권 표시에 넣기
2. **앱 ID(패키지 이름)**: 지금은 `com.balranyang.game` 입니다. **스토어에 올린 뒤에는 바꿀 수 없습니다.** 본인 도메인/이름 기반(`kr.co.○○.balranyang` 등)으로 바꾸려면 알려 주세요(파일 몇 곳을 일괄 수정합니다).
3. 개인 개발자인지 사업자(회사)인지 — 개인 계정이면 아래 안드로이드 14일 테스트 규칙이 적용됩니다.

## 2. Google Play (안드로이드)
**비용**: 개발자 등록 25달러(1회)
1. play.google.com/console 에서 개발자 계정 등록(본인 확인·결제). 개인 계정은 2023-11-13 이후 가입자라면 **프로덕션 출시 전에 비공개 테스트에 테스터 12명 이상이 14일 연속 참여**해야 합니다(구글 도움말 기준). 주변 지인 테스트를 이 용도로 쓰세요.
2. 업로드 키 만들기(1회, 분실 주의): `keytool -genkey -v -keystore balranyang.keystore -alias balranyang -keyalg RSA -keysize 2048 -validity 10000`
3. GitHub 저장소 → Settings → Secrets에 등록: `ANDROID_KEYSTORE_BASE64`(키스토어를 base64로 변환한 값), `ANDROID_KEYSTORE_PASSWORD`, `ANDROID_KEY_ALIAS`, `ANDROID_KEY_PASSWORD`
4. Actions → "Android build" → Run workflow → 결과물 `balranyang-release-aab` 내려받기
5. Play Console → 앱 만들기 → 비공개 테스트 트랙에 AAB 업로드, 테스터 12명 이메일 등록
6. 앱 콘텐츠 설문(개인정보·데이터 보안·광고·콘텐츠 등급·타겟 연령) → `store-forms.md` 답안 참고
7. 스토어 등록정보: `listing_ko.md` 문구, `app-icon-512.png`, `feature-graphic-1024x500.png`, `screenshots/android/*`
8. 14일 후 "프로덕션 액세스 신청" → 심사(보통 수일) → 출시

## 3. App Store (iOS)
**비용**: Apple Developer Program 연 99달러(한국 원화 결제 시 약 13만 원대, 가입 화면 가격 기준)
**필요**: 빌드·서명을 하려면 **Mac + Xcode**가 필요합니다. Mac이 없다면 Codemagic 같은 클라우드 빌드 서비스(유료/무료 한도)나 GitHub Actions macOS 러너에 인증서를 등록하는 방법이 있습니다(원하시면 설정해 드립니다).
1. developer.apple.com 에서 Apple Developer Program 가입(본인 확인 수일 걸릴 수 있음)
2. App Store Connect에서 앱 생성(번들 ID = 앱 ID)
3. Mac에서 `npm ci && npx cap sync ios && npx cap open ios` → Xcode에서 Team 선택 → Product > Archive → 업로드
4. TestFlight로 내부/외부 테스트(지인 테스트에 사용 가능) → 앱 정보 입력(`listing_ko.md`, `screenshots/ios/*`, 개인정보 "수집 안 함", 연령 등급)
5. 심사 제출. **심사 주의**: 웹 화면만 감싼 앱은 가이드라인 4.2(최소 기능)로 거절될 수 있습니다. 발라냥은 완결된 게임 콘텐츠·오프라인 동작·햅틱·전용 아이콘/시작화면을 갖췄고, 심사 메모에 "오프라인 퍼즐 게임, 계정·광고·결제 없음"을 명시하세요.

## 4. 출시 후/다음 단계
- [ ] 결제(코인 주머니 등) 추가: 구글 결제·애플 인앱결제 연동 + 확률형 아이템 정보 표시 + 결제 시 보호자 확인(이미 어른 확인 화면 있음)
- [ ] 온라인 랭킹(서버 필요) 추가 시 개인정보 방침·데이터 안전 설문 갱신
- [ ] 앱 아이콘 최종본(1024×1024 원본 일러스트로 다시 내보내기 — 현재 아이콘은 512를 확대한 것이라 가장자리가 약간 부드러움)
- [ ] 실제 기기 테스트: 저사양 안드로이드에서 시작 애니메이션 성능, 아이폰 소리(무음 스위치)

## 5. 예상 일정(참고)
| 단계 | 기간 |
|---|---|
| 계정 가입·본인 확인 | 1~7일 |
| 안드로이드 비공개 테스트(개인 계정 규칙) | 14일 이상 |
| 심사 | 구글 수일, 애플 1~3일(첫 심사는 더 걸릴 수 있음) |
