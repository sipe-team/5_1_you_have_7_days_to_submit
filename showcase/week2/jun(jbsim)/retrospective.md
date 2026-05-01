# WebPage to PNG — 회고

## 스펙 판단
- 넣으려다 뺀 기능: 자동 본문 영역 감지 — article 태그나 readability 알고리즘으로 본문만 잘라내는 기능. 사이트마다 마크업이 너무 달라서 일관성 확보가 불가능.
- 넣었는데 후회한 기능: CLI 옵션 과잉 — --overlap, --quality, --format, --viewport-width, --wait-strategy... 실제로는 90% 디폴트만 씀

## 효율 돌아보기
- 이렇게 했으면 더 좋았을 것: 첫날부터 device_scale_factor=2 디폴트 — 1배로 찍은 PNG는 Claude한테 던지면 텍스트 인식률이 눈에 띄게 떨어짐, 나중에 재캡처하느니 처음부터 하는게 나음
- AI 활용에서 효과적이었던 점: 추상적인 "테스트해줘"가 아니라 실제 페이지 URL을 주고 결과 PNG를 보여주면서 피드백 받기. hallucination이 확연히 줄어듦.
- AI 활용에서 비효율적이었던 점: "Playwright로 스크린샷 도구 만들어줘" 식 추상 프롬프트 — 매번 다른 디폴트, 다른 라이브러리 버전 코드가 나옴. 재현성 0.
