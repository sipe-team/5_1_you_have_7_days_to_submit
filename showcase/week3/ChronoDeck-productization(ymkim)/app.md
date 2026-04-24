# ChronoDeck 제품화

## 한 줄 소개
> Apple Watch와 iPhone으로 macOS 단축키를 실행하는 ChronoDeck을 실제 배포 가능한 제품으로 고도화

## 문제 정의
첫주차에는 iPhone, Apple Watch, macOS를 연결해 키보드 리모컨으로 동작하는 MVP를 만들었다.
하지만 실제 사용자가 설치해서 쓰려면 기능 구현만으로는 부족했다.

macOS 앱은 메뉴바 앱으로 자연스럽게 동작해야 했고, 키 입력/페어링/접근성 권한/업데이트/DMG 배포가 안정적이어야 했다.
iOS와 watchOS도 App Store 심사를 통과할 수 있도록 번들 ID, 개인정보 매니페스트, 로컬 네트워크 설명, 다국어 문자열을 정리해야 했다.
이번 주는 ChronoDeck을 "동작하는 프로토타입"에서 "배포 가능한 제품"으로 끌어올리는 데 집중했다.

## 링크
- 소스코드: https://github.com/BearMett/ChronoDeck
- 랜딩 페이지: https://github.com/BearMett/chronodeck-landing
- 릴리즈 피드: https://github.com/BearMett/chronodeck-releases

## 기술 스택
| 영역 | 선택 | 선택 이유 |
|------|------|----------|
| iOS/watchOS | SwiftUI, WatchConnectivity | iPhone을 설정/중계 허브로 두고 Watch는 얇은 리모컨 UI로 유지 |
| macOS | SwiftUI, AppKit, 메뉴바 앱 | 키 이벤트 실행, 접근성 권한 확인, 로컬 네트워크 서버, 메뉴바 상주 UX가 필요 |
| 통신 | Bonjour, WebSocket, WatchConnectivity | 같은 네트워크의 Mac을 찾고 iPhone/Watch/Mac 사이 명령을 전달 |
| 배포 | App Store, 직접 배포 DMG, Sparkle | iOS/watchOS는 App Store, macOS는 DMG와 자동 업데이트로 배포 |
| 랜딩 | Next.js | 제품 설명, 다운로드, 개인정보 처리방침, 다국어 페이지를 빠르게 구성 |
| AI 활용 | Claude Code, v0 | Swift 앱 고도화와 랜딩 페이지 초안/카피 개선에 활용 |

## 이번 주 타임라인
| 요일 | 작업 내용 | 소요 시간 |
|------|----------|----------|
| 월 | macOS 앱을 메뉴바 전용 앱으로 전환, 페어링 UX와 키 입력 편집 흐름 개선 | |
| 화 | Sparkle 자동 업데이트 통합, DMG 배포 채널과 빌드 스크립트 정리 | |
| 수 | Watch 제스처 설정, 업데이트 UI, 릴리즈 DMG 스킬/문서화, 랜딩 페이지 초기 구성 | |
| 목 | 랜딩 페이지 다국어 라우팅, 카피 개선, 다운로드 버튼 추적, 개인정보 처리방침 추가 | |
| 금 | iOS/watchOS/macOS 로컬라이제이션, 개인정보 매니페스트, 번들 ID, App Store 심사 거부 사유 대응 | |
| 토 | 제품 소개/다운로드 경로 점검, 릴리즈 피드와 앱 아이콘 정리 | |
| 일 | 쇼케이스와 회고 작성 | |
