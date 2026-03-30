# ChronoDeck

## 한 줄 소개
> iPhone과 Apple Watch를 macOS용 커스텀 키보드/리모컨으로 만드는 Stream Deck 스타일 앱

## 문제 정의
macOS에서 발표나 데모를 진행할 때 키보드에 직접 손이 닿기 어려운 상황이 많다. 
기존 리모컨은 슬라이드 넘김 정도만 가능하고, Stream Deck은 별도 하드웨어가 필요하다. 
iPhone과 Apple Watch를 범용 매크로 리모컨으로 활용하면 추가 장비 없이 커스텀 키 조합을 실행할 수 있다.

## 링크
- 앱스토어 예정
- MacOS 앱 링크 예정

## 기술 스택
| 영역 | 선택 | 선택 이유 |
|------|------|----------|
| iOS/watchOS | SwiftUI (Liquid Glass) | iOS 26 디자인 시스템 적용, Watch 컴패니언 지원 |
| macOS | Swift 네이티브 앱 | 키 이벤트 수신 및 실행을 위한 companion 앱, 필요 시 인터넷 배포 |
| 통신 | 네트워크 기반 (Bonjour 등) | 같은 네트워크 내 iOS/Watch → macOS 명령 전달 |
| 배포 | App Store + macOS 직접 배포 | iOS/watchOS는 App Store, macOS는 필요에 따라 패키지 배포 |
| AI 활용 | Claude Code로 전체 구현, Stitch로 화면 구성 |  |

## 이번 주 타임라인
| 요일 | 작업 내용 | 소요 시간 |
|------|----------|----------|
| 월 | 스펙 정리, 기능 설계, 이슈 생성 | |
| 화 | iOS 앱 + Watch 앱 구현 (키 설정 UI, 리모컨 화면) | |
| 수 | macOS companion 앱 구현 (키 이벤트 수신/실행) | |
| 목 | 테스트, 폴리싱, 배포 준비 | |
| 금 | 배포 테스트, App Store 심사 제출 | |
| 토 | | |
| 일 | 쇼케이스 작성 | |
