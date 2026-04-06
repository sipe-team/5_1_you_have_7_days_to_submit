# Terminal AI Watcher

## 한 줄 소개
> AI CLI 도구(Claude Code, Codex, Gemini CLI)의 작업 완료·권한 요청을 IDE 알림으로 받아주는 IntelliJ 플러그인

## 문제 정의
Claude Code, Codex, Gemini CLI 같은 AI 터미널 도구를 쓰다 보면, 작업이 오래 걸릴 때 다른 일을 하게 된다.
그런데 작업이 끝나거나 권한 승인이 필요한 시점을 놓치면 대기 시간이 길어진다.
기존에는 터미널을 직접 들여다보는 수밖에 없었고, IDE 내장 터미널에서는 알림 수단이 아예 없었다.

이 플러그인은 각 AI CLI 도구의 **Hook 시스템**을 활용해 이벤트를 감지하고,
IDE 풍선 알림, macOS 시스템 알림,Dock 배지, 사운드 4채널로 알려준다.
터미널 출력을 파싱하지 않고 공식 Hook을 쓰기 때문에 오탐이 없다.

## 링크
- 서비스: https://plugins.jetbrains.com/plugin/30937-terminal-ai-watcher
- 소스코드: https://github.com/simuelunbo/intelli_J_terminal_alert

## 기술 스택
| 영역 | 선택 | 선택 이유 |
|------|------|----------|
| 언어 | Kotlin | IntelliJ Platform 공식 언어, 코루틴 기반 비동기 처리에 적합 |
| 플랫폼 | IntelliJ Platform SDK (build 243+) | Android Studio·IntelliJ IDEA 동시 지원, 플러그인 생태계 활용 |
| UI | Jetpack Compose + Jewel 디자인 시스템 | IDE 네이티브 룩앤필, Swing DSL 폴백으로 호환성 확보 |
| 직렬화 | kotlinx-serialization-json | CLI Hook에서 오는 JSON 페이로드 파싱, 멀티 필드 매핑 |
| 통신 | 내장 HTTP 서버 (com.sun.net.httpserver) | CLI Hook → 플러그인 이벤트 수신, 동적 포트 할당으로 다중 IDE 인스턴스 지원 |
| 배포 | JetBrains Marketplace | IntelliJ 기반 IDE 공식 배포 채널 |
| AI 활용 | Claude Code로 전체 구현 | Hook 설정 스크립트·이벤트 파싱·알림 디스패치 로직 전반 |


