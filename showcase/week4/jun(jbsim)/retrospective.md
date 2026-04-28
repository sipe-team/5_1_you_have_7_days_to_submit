# WaveCatch — 회고

### 잘한점

1. 코어와 GUI를 처음부터 분리한 것

downloader.py를 “Qt를 모르는 순수 모듈”로 두고, GUI는 콜백·QThread로 감싸기만 했음                                                       
- yt-dlp 옵션을 바꿀 때 GUI 코드를 건드릴 필요가 없었다.
- 단위 테스트를 PySide 의존성 없이 돌릴 수 있었다.                                                                                                                                                                      
- 향후 CLI 모드나 다른 프런트엔드(웹·메뉴바 앱)로 재사용할 여지를 남겼다.

2. ffmpeg 자동 탐지 (find_ffmpeg)
.app 번들로 실행하면 셸 PATH가 비어 ffmpeg을 못 찾는 함정이 있다. 
Homebrew 표준 경로 → /usr/local/bin → PATH 순서로 폴백을 둬, 사용자가 “왜 변환만 실패하지?”로 헤매는 시간을 없앴다.

### 아쉬운점

ffmpeg을 외부 의존으로 둔 트레이드오프
- 번들 미포함 → 용량 작고 라이선스 깔끔, 그러나 brew install ffmpeg을 모르는 사용자에겐 또 하나의 허들