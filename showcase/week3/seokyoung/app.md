# Music Digging

## 한 줄 소개
> Bandcamp·SoundCloud·웹 매거진 신보를 사용자 취향 공식(`rules/digging.md`)에 맞춰으로 매주 묶어 Spotify 플레이리스트로 동기화하는 음악 발굴해주는 자동화. 

## 문제 정의
03-24 버전의 `weekly-dig.sh`는 한 번의 `claude -p` 호출에 수집(WebSearch)부터 점수화·큐레이션·글쓰기까지 전부 위임했다. 매주 동작은 했지만 — 수집이 막히면 분석까지 죽고, 같은 데이터에 프롬프트만 바꿔 재실행할 수 없고, "왜 이 곡이 추천됐나"가 LLM 한 번의 응답 안에 갇혀서 추적이 어려웠다. 

현재 구조가 맞나 전체적으로 리뷰한 뒤, 팀원들 피드백을 받아 이미 있는 추천 모델을 사용하기로 했다. 알고리즘을 텍스트 임베딩 + Last.fm 그래프로 잠그면서(audio-features deprecation) sentence-transformers 생태계가 Python 중심이라는 사실에 맞춰 자동화 스택을 Python으로 올렸다. 기존에서 **데이터 흐름 한 폴더만 갈아끼우는 것**이 목표였기 때문에 `skills/` 에이전트 정의·`rules/digging.md` 공식·weekly md 출력 형식·Spotify OAuth(`scripts/auth.js`)는 의도적으로 손대지 않았고, 같은 후보 풀에 같은 weekly(글쓰기 차이 외)가 거의 동일하게 나오는 게 목표였다.

## 폴더 구조

```
music-digging/
├── CLAUDE.md
├── README.md
├── rules/                     # 작업별 규칙 (LLM 컨텍스트)
│   ├── digging.md             # 취향 공식
│   ├── automation.md          # 자동화 룰
│   ├── blog.md
│   ├── ai-orchestration.md
│   └── app.md                 ← 본 파일
├── skills/                    # Claude 에이전트 정의 (curate가 참조)
│   ├── trend-scout.md
│   ├── taste-analyst.md
│   └── connector.md
├── pipeline/                  ← NEW — Python 자동화 5단계
│   ├── collect.py             # [1] RSS/API/스크래핑 → reference/trending/{date}.json
│   ├── score.py               # [2] 임베딩 + Last.fm 그래프 → trending/{date}.scored.json
│   ├── curate.py              # [3] Claude CLI 호출 래퍼 → weekly/{date}.md
│   ├── sync.py                # [4] Spotify search + playlist (구 spotify-sync.js 포팅)
│   ├── feedback.py            # [5] Spotify 활동 → input/taste-input.md 갱신
│   └── lib/
│       ├── spotify.py
│       ├── lastfm.py
│       ├── embedding.py       # bge-m3 또는 OpenAI
│       ├── parsing.py         # weekly md 파서 (구 parseWeeklyDig)
│       └── cache.py           # taste-centroid, embedding 디스크 캐시
├── scripts/
│   ├── weekly-dig.sh          # 5단계 오케스트레이션 진입점
│   └── auth.js                # Spotify OAuth 브라우저 팝업 (JS 유지)
├── input/
│   └── taste-input.md         # 사용자 취향 입력 (feedback이 갱신)
├── profile/                   # 분석 산출물
│   ├── taste-profile.md
│   └── korean-underground-dig.md
├── reference/
│   ├── trending/              ← NEW 산출물 (JSON 중간 단계)
│   │   ├── {date}.json
│   │   └── {date}.scored.json
│   └── connection-map/        # 연결망 (curate 입력)
├── weekly/                    # curate 산출물 (md)
├── log/
│   ├── 2026-03.md
│   ├── orchestration-review.md
│   ├── retrospective.md
│   └── retro-2026-05-01.md
├── pyproject.toml             ← NEW
├── .python-version            ← NEW (3.11+)
└── .env / scripts/.tokens.json (gitignored)
```

**손대지 않은 것**: `skills/`, `rules/digging.md`, weekly md 출력 형식, `scripts/auth.js`.
**갈아끼운 것**: `scripts/spotify-sync.js` → `pipeline/sync.py` (동작 동일성 유지 포팅), `weekly-dig.sh` 내부의 단일 `claude -p` 호출 → 5단계 순차 호출.
**새로 생긴 것**: `pipeline/`, `reference/trending/*.json`, `pyproject.toml`, `.python-version`.
