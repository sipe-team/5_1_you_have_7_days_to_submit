# WebPage to PNG

## 한 줄 소개
> WebPage to PNG

## 문제 정의
스크롤이 가능한 웹페이지를 PNG로 길게 이어서 보여지는 형식이 아닌 부분 부분 나눠서 한눈에 볼 수 있는 PNG 형태로 보여지도록 하고 싶어서 만든 툴
접근 불가능한 페이지를 claude code 등 AI가 확인 할 수 있도록 하기 위해 만든 툴


## 기술 스택
| 영역 | 선택 | 선택 이유 |
|------|------|----------|
| 언어 | python | Playwright/Pillow 등 같은 핵심 의존성이 모두 1차 지원되고 Claude Code에서 마찰 없이 실행,확장에 적합 |
| 브라우저 자동화 + 풀페이지 스크린샷 | Playwright | full_page=True 한 줄로 전체 페이지 캡처가 끝나고, device_scale_factor=2로 Retina 화질 캡처 가능. async API가 메인이라 lazy loading/SPA 대응이 안정적이고 Selenium보다 빠름. add_style_tag로 sticky 헤더 제거 같은 트릭도 한 줄 |
| 이미지 분할 | Pillow (PIL) | crop()만 써서 원본 픽셀 그대로 잘라내면 화질 손실 0. 무거운 OpenCV 쓸 일이 아니고, Python 이미지 처리의 사실상 표준 |
| CLI 인터페이스 | Typer | 타입 힌트 기반이라 Kotlin에서 넘어온 입장에 자연스럽고, 자동 --help 생성과 검증이 공짜. argparse보다 코드량 적고 Click보다 모던함 |
| 비동기 런타임 | asyncio | Playwright async API의 전제. wait_for_function으로 폰트 로딩 완료 같은 비동기 조건 대기에 필수 |

