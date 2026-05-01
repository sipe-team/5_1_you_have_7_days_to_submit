# Swim Dots HK — 회고

- 잘된 점: 앱을 열면 권한 한 번 승인 → 곧바로 워크아웃 목록으로 진입하는 흐름을 확인하면서 XML 파싱·청크 단위 사전 필터링·AsyncStorage 캐시 코드가 전부 필요 없어졌고, HealthKit 쿼리 자체가 충분히 빨라 "데이터 소스를 HealthKit으로 갈아끼우자"는 큰 방향이 실기기에서 검증됐다.
- 잘 안 된 점: 영민님 Apple Developer 팀 명의로 바로 실배포할 계획이었지만 App Store Connect 권한 이슈로 헤매다, 7일 무료 프로비저닝으로 테스트 라운드만 먼저 돌리고 권한이 풀린 뒤 실배포로 가는 우회 경로를 한 번 거쳤다.
- 배운 점: 변형 fork에서는 "바뀌는 것"보다 "그대로 두는 것"의 목록을 spec에서 먼저 못 박는 게 핵심이라, `SwimWorkout`/`SwimLap` 타입·`HalftoneCanvas`·`StrokeDots`·`ArtScreen`/`WorkoutListScreen`·`useState` 기반 네비게이션·가로 FlatList 스와이프를 0줄 수정으로 가져온 채 데이터 레이어 한 폴더만 갈아치우자, 두 앱의 같은 워크아웃 도트가 거의 동일하게 그려진다는 사실로 그 결정이 검증됐다.
