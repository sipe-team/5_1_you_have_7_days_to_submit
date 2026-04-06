# Terminal AI Watcher — 회고

## 스펙 판단
- 넣으려다 뺀 기능: Windows/Linux 알림 지원 (macOS 전용으로 범위 축소)
- 넣으려다 뺀 기능: 터미널 출력 파싱 기반 감지 (Hook 기반으로 전환하면서 완전히 제거)
- 빼서 다행인 기능: 터미널 출력 파싱 — Hook 방식이 오탐 제로이고 CLI 도구 업데이트에도 깨지지 않음
- 넣었는데 후회한 기능: Compose UI + Swing DSL 듀얼 구현 — 호환성은 좋지만 유지보수 포인트가 두 배 (하지만 추후 Intelli J에서 Compose로 UI 완벽 지원 할 경우 쉽게 마이그레이션 가능)

## 효율 돌아보기
- 이렇게 했으면 더 빨랐을 것: Compose UI 없이 Swing DSL만으로 시작했으면 하루는 절약. 설정 화면은 단순해서 Compose가 오버엔지니어링이었음
- AI 활용에서 효과적이었던 점: Claude Code로 Hook 설정 스크립트(bash curl 명령, PPID 체인 워킹) 생성이 빨랐음. IntelliJ Platform API 문서를 직접 찾는 것보다 코드 생성 후 수정하는 방식이 훨씬 효율적
- AI 활용에서 비효율적이었던 점: IntelliJ Platform 플러그인 개발은 문서가 부족하고 버전별 차이가 커서, AI가 생성한 코드가 deprecated API를 쓰는 경우가 잦았음. 특히 Terminal API 접근 방식에서 여러 번 시행착오

