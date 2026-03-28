# 참여 가이드라인

## 시작하기

1. 이 저장소를 클론합니다
2. `members/{본인-github-id}/` 폴더를 생성합니다
3. `profile.md`를 작성합니다 (템플릿: [templates/profile.md](templates/profile.md))
4. PR을 올려 자기소개를 완료합니다

## 주간 워크플로우

### 출하 주 (1, 2, 4, 5주차)

```
월요일    스펙 정리 → PR로 공유 (draft 가능)
화~목     구현 (코드는 외부 저장소에서 관리)
금요일    배포 / 심사 제출
토요일    폴리싱
일요일    제품 소개서 작성 → PR 오픈 (마감: 일요일 자정)
```

1. 브랜치 생성: `{github-id}/week{N}`
2. `members/{github-id}/apps/week{N}-{앱이름}/` 폴더 생성
3. `README.md` (제품 소개서) 작성 (템플릿: [templates/app.md](templates/app.md))
4. 스크린샷은 같은 폴더의 `screenshots/`에 저장
5. PR 오픈
   - 제목: `[week{N}] {앱이름} — {github-id}`
   - 마감: **매주 일요일 자정**

### 회고 주 (3, 6주차)

1. 브랜치 생성: `{github-id}/cycle{N}`
2. `members/{github-id}/retrospectives/cycle-{N}.md` 작성 (템플릿: [templates/retrospective.md](templates/retrospective.md))
3. PR 오픈
   - 제목: `[cycle{N}] 회고 — {github-id}`

## 브랜치 규칙

- `main` 직접 push 금지
- 브랜치명: `{github-id}/week{N}` 또는 `{github-id}/cycle{N}`
- PR을 통해서만 main에 머지

## 커밋 컨벤션

| 접두사 | 용도 |
|--------|------|
| `docs:` | 제품 소개서, 회고 작성/수정 |
| `chore:` | 프로필, 설정 파일 등 |
| `asset:` | 스크린샷, 이미지 추가 |

예시: `docs: week1 제품 소개서 작성`

## PR 리뷰 규칙

- 다른 멤버의 PR에 **최소 1개 코멘트** (정기 모임 전까지)
- 코멘트 예시:
  - "이 기능은 빼도 되지 않았을까?" (스펙 피드백)
  - "실제로 써봤는데 이 부분이 좋았다" (사용 후기)
  - "다음에는 이런 스택도 고려해보면 어떨까" (기술 피드백)

## 정기 모임

- 매주 [요일] [시간] 온라인
- **출하 주:** 제품 데모 5분 + 피드백 5분 (인당)
- **회고 주:** 사이클 회고 공유 + 다음 사이클 스펙 브레인스토밍
