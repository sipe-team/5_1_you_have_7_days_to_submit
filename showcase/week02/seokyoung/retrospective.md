# Swim Dots — 회고


## 진행 단계 
| Task | 내용 | 테스트 |
|------|------|------|
| 1 | Expo 프로젝트 + 의존성 | — |
| 2 | 데이터 타입 (SwimWorkout, SwimLap, StrokeType) | — |
| 3 | Jest 설정 + 샘플 XML | — |
| 4 | XML 파서 + 포맷 유틸 | 21 |
| 5 | 하프톤 도트 생성 + 영법 색상 (TDD) | 8 |
| 6 | 파일 선택 화면 + AsyncStorage 훅 | — |
| 7 | 워크아웃 목록 + StrokeDots | — |
| 8 | Skia 하프톤 캔버스 | — |
| 9 | 아트 스크린(스와이프 + 공유) + App 네비게이션 | — |

## 스펙 판단
### **넣으려다 뺀 기능**
- HealthKit 직접 연동(유료 계정 필요), React Navigation, Android 빌드, 워크아웃 비교/통계 화면, 서버 백업.

### **빼서 다행인 기능**:
- **HealthKit**
  - $99/년 가입 없이 Apple Health XML 내보내기 파일을 직접 선택하는 방식으로 우회. MVP에 전혀 지장 없고, 유료 계정 확보 후 교체할 수 있는 인터페이스로 설계.
  - 다만... 헬스 데이터 파일이 640MB라... 앱보다 더 큰 헬스 데이터. 웹에서 할 때는 스크립트로 수영 데이터만 추출해서 넣을 수 있었는데, 앱은 그게 안 되니 청크 단위 사전 필터링으로 로딩 속도를 줄여보고자 했음. HealthKit 연동하면 이 모든 게 무의미해질 부분이라 적당한 선에서 마무리.
### **넣었는데 후회한 기능**:
  - **`expo-dev-client`** — Expo 공식 문서 따라 추가했다가 SDK 54/RN 0.81 Swift API 충돌로 전부 제거. `expo run:ios`는 dev-client 없이도 네이티브 빌드가 되므로 애초에 불필요했음.

### 해결한 주요 이슈 (DEBUGGING.md 요약)
- Xcode 라이선스 에러 69 (`sudo xcodebuild -license accept`)
- Expo Go + Skia 비호환 → `expo run:ios` 네이티브 빌드로 전환
- `expo-dev-client@55`가 SDK 54/RN 0.81에 Swift API 충돌 → 제거
- 한글 파일명 URI percent-encoding → `decodeURIComponent`
- `expo-file-system` 새 File API가 640MB 미지원 → `expo-file-system/legacy`로 청크 읽기
- p5.js `ellipse(diameter)` vs Skia `Circle(radius)` — 점이 2배 크게 그려짐 → diameter/2


## 돌아보기