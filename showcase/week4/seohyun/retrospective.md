# StealthTicker — 회고

## 스펙 판단
- 넣으려다 뺀 기능: Webview 기반 차트 (Chart.js), Marketplace 정식 배포
- 빼서 다행인 기능: Webview 차트. Unicode sparkline으로도 충분히 의도가 전달됨
- 넣었는데 후회한 기능: 기능이 적어서 없음...

## 효율 돌아보기
- 이렇게 했으면 더 빨랐을 것: VS Code Extension API 공식 문서를 먼저 훑고 시작했으면 시행착오가 줄었을 것
- AI 활용에서 효과적이었던 점: Extension 활성화 로직, StatusBarItem 생성, HoverProvider 연동 코드 빠르게 작성
- AI 활용에서 비효율적이었던 점: API 응답 파싱은 실제 데이터를 직접 확인하며 수정해야 해서 AI 도움이 제한적이었음

## 다음 주에 가져갈 것
- 처음 접하는 플랫폼일수록 AI보다 공식 문서를 먼저 보는 게 효율적
