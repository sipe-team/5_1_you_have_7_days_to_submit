# Terminal AI Watcher — 회고

  - 잘된 점: 우선순위 모델을 "정확도 > 침묵"에서 "항상 표시 > 정확도"로 뒤집고 5-tier fallback 끝에 legacy 동작을 보존한 것이 이번 작업을 회귀에서 구해냈다.                                                                
  - 잘 안 된 점: 실행 환경이 Reworked Terminal default(2025.2+)라는 사실을 코드 작성 전에 확인하지 않고 Classic Terminal API 가정으로 zip을 빌드한 탓에, IDE 재설치·CLI 재시작 비용을 다섯 사이클 동안 반복했다
  - 배운 점: reflection으로 frontend/backend 분리라는 아키텍처 한계를 우회하려 수백 줄을 쌓았지만 결국 1줄 fallback이 가치를 만들었던 것 — 막힌 길에서 코드 길이가 늘어날수록 비용만 커지고 복잡도는 우회의 정당성을 보장하지 않는다.