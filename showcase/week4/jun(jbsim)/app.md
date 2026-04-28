# WaveCatch

## 한 줄 소개
> 영상 URL 한 줄을 붙여 넣으면 오디오만 깔끔하게 뽑아 WAV/MP3/원본으로 저장해 주는 macOS 데스크톱 앱. 

## 문제 정의
음악·강연·인터뷰 영상에서 오디오만 따로 보관하고 싶을 때 사용
 yt-dlp + ffmpeg CLI 직접 사용 — 가장 강력하지만, 매번 옵션을 외워야 하고, 비개발자 가족·지인에게 권하기 어려움 

## 기술 스택
  | 영역 | 선택 | 선택 이유 |
  |------|------|----------|                                                                                                                                                                                                
  | 다운로드 엔진 | yt-dlp (>=2025.3.31) | 사이트 변경에 가장 빠르게 대응되는 사실상 표준. `bestaudio/best` + `noplaylist` 조합으로 최소 옵션·최대 호환. |
  | 오디오 변환 | ffmpeg (외부 의존) | yt-dlp `FFmpegExtractAudio` 후처리기로 WAV·MP3 무손실/고품질(`preferredquality="0"`) 추출. 번들 대신 시스템 설치를 요구해 라이선스·용량·최신성 모두 확보. |                          
  | GUI | PySide6 (Qt 6) | 파이썬 생태계와 yt-dlp를 그대로 쓰면서도 진짜 네이티브 위젯·스레드(QThread) 활용 가능. Tk/PyQt 대비 라이선스(LGPL)·디자인 자유도 균형이 가장 좋음. |                                             
  | 디자인 시스템 | Wavecatch Design System (자체 토큰) + Lucide 아이콘 (MIT) | `ui/tokens.py`에 컬러·반경·여백을 토큰화하고 `ThemeManager`로 라이트/다크 동적 전환. 아이콘은 Lucide SVG로 통일감 확보. |                   
  | 비동기 처리 | QThread (`DownloadWorker`, `ProbeWorker`) | UI 멈춤 없이 다운로드 진행률·메타 프리뷰를 실시간 갱신. 시그널/슬롯으로 GUI와 단방향 통신. |                                                                  
  | 진행 표시 | 자체 ProgressRing 위젯 | 막대 대신 원형 링 — 다운로드/변환/완료 상태 전이가 한 컴포넌트에서 표현됨. |                                                                                                       
  | 패키징 | PyInstaller 6.19 + `Wavecatch.spec` + `make_dmg.sh` | `.app` 번들 → `.dmg` 까지 단일 명령. Apple Silicon(arm64) 단일 타깃으로 좁혀 빌드 단순화·용량 축소(≈48 MB). |                                            
  | 영속화 | QSettings | 마지막 저장 폴더·테마 등 사용자 설정만 보관. 키체인·파일 수정 일체 없음(전역 보안 규칙 준수). |                                                                                                    
  | 테스트 | pytest (`tests/test_downloader.py`, `manual_smoke.py`) | 다운로드 로직(`downloader.py`)을 GUI에서 분리해 단독 테스트 가능하도록 설계. |   



