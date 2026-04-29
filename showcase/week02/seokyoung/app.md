# Swim Dots

## 한 줄 소개
> Apple Watch 수영 기록을 하프톤 도트 아트로 시각화하는 iOS 앱.

## 문제 정의
수영 워크아웃 데이터는 페이스·심박·영법 같은 숫자만 쭉 나열되어 있고, 한 번의 수영이 "어떻게 느껴졌는지"를 남기기 어렵다. 앱을 만들기 전, p5.js + p5.riso로 웹에서 만든 하프톤 시각화가 꽤 좋았기 때문에 iPhone에서 바로 꺼내보고 공유할 수 있으면 훨씬 쓰임새가 있겠다 싶어. iOS 앱에 도전했다. (네이티브는 아니고 그저 RN..)

Apple Developer 유료 계정($99/년)이 없어 HealthKit 직접 연동은 못 하는 상황이라, **Apple Health 내보내기 XML을 직접 파일로 선택 → 파싱 → Skia로 렌더 → 공유 시트**의 경로로 우회했다. Xcode 무료 프로비저닝(7일 유효)으로 실기기에 설치해서 사용 가능. (을 나중에 알아서, 시뮬레이터로만 확인했음 😂)

## 링크
- 소스코드: https://github.com/samseburn/swim-dots
- 앱스토어 등록: 유료 계정 확보 후 진행 예정 (영민님께 감사~)

## 기술 스택
| 영역 | 선택 | 선택 이유 |
|------|------|----------|
| 프론트엔드 | React Native + Expo SDK 54 + TypeScript | 웹(React) 경험 그대로 활용. Expo로 빌드/설정 오버헤드 최소화 |
| 렌더링 | @shopify/react-native-skia | GPU 가속으로 60fps 렌더링. p5.js의 `ellipse` 호출 포팅 용이 |
| 백엔드 | 없음 (AsyncStorage 캐싱) | 개인 데이터. 파싱 결과만 로컬에 저장해 다음 실행에 즉시 목록 표시 |
| 배포 | Xcode 무료 프로비저닝 (실기기, 7일 유효) | Apple Developer 미가입 상태. 추후 실배포 예정 |
| AI 활용 | Claude Code — 9개 Task 분할 + TDD(순수 함수 먼저 테스트) + 디버깅 기록 자동화 | 대용량 XML 파싱, 좌표계 변환 등 돌다가 깨질 곳이 많아 테스트로 먼저 잡고 UI는 시뮬레이터에서 수동 확인 |

### 핵심 기술 선택
- **fast-xml-parser**: 순수 JS, 네이티브 모듈 불필요. Expo Go 호환성 고민 없이 사용. (나중에 HealthKit 연동을 하게 되면 필요없음)
- **청크 단위 사전 필터링 (expo-file-system legacy)**: Apple Health 전체 내보내기가 640MB라 `text()` 한 방으로 하면 `string length exceeds limit` (...) 파일을 2MB씩 끊어 읽으면서 `<Workout>` 태그만 스캔 → 수영 워크아웃만 누적해서 기존 파서에 전달.
- **라이브러리 없는 네비게이션**: 화면이 3개뿐(파일 선택 / 워크아웃 목록 / 아트)이라 `useState<Screen>` 하나로 충분. React Navigation 의존성 제외.
- **가로 FlatList + pagingEnabled**: 아트 스크린 스와이프를 전용 라이브러리 없이 FlatList 기본 기능으로 해결. → 요건 몰랐는데 좋네요..
