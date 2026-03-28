# 참여 가이드라인

## 시작하기

1. 이 저장소를 클론합니다
2. `members/{이니셜}/` 폴더를 생성합니다
3. `profile.md`를 작성합니다 (템플릿: [templates/profile.md](templates/profile.md))
4. PR을 올려 자기소개를 완료합니다

## 주간 워크플로우 (예시)

```
월요일    스펙 정리 → PR로 공유 (draft 가능)
화~목     구현 (코드는 외부 저장소에서 관리)
금요일    배포 / 심사 제출
토요일    폴리싱
일요일    쇼케이스 작성 → PR 오픈 (마감: 일요일 자정)
```

1. 브랜치 생성: `{이니셜}/week{N}`
2. `showcase/week{N}/{앱이름}({이니셜})/` 폴더 생성
3. `app.md` 작성 (템플릿: [templates/app.md](templates/app.md))
4. `retrospective.md` 작성 (템플릿: [templates/retrospective.md](templates/retrospective.md))
5. PR 오픈
   - 제목: `[week{N}] {앱이름} — {이니셜}`
   - 마감: **매주 일요일 자정**

## 브랜치 규칙

- 브랜치명: `{이니셜}/week{N}`

## 정기 모임

- 주 단위로 [요일] [시간] 오프라인 우선
- **출하 및 회고:** 
1. 제품 데모 + 피드백 5분
2. 사이클 회고 공유 + 다음 사이클 스펙 브레인스토밍
