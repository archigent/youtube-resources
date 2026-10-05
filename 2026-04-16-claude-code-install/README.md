# 클로드 코드 설치 + 지침 세팅 — 5분이면 터미널도 두렵지 않습니다

▶ 영상: https://youtu.be/oqPeARv4_Os

---

[1] 설치 & 실행 명령어

▶ Windows (PowerShell)
  Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass -Force
  npm install -g @anthropic-ai/claude-code

▶ Mac
  brew install node && npm install -g @anthropic-ai/claude-code

▶ 실행
  claude
  → 브라우저 자동 열림 → Anthropic 로그인 → Authorize → "Logged in" 확인

※ Windows는 Git for Windows 필수: https://git-scm.com/downloads/win
※ 설치 전 Node.js LTS 설치: https://nodejs.org

[2] CLAUDE.md 대화로 만드는 문장 (복붙)

▶ 복붙 프롬프트
  CLAUDE.md 파일 만들어줘. 내 규칙은 이렇게: 한국어로 답하고, 결과는 3줄 이내로 간결하게, 설명보다 결과 우선, 파일 수정 전에는 먼저 물어볼 것.

→ "내 규칙은 이렇게:" 뒤만 본인 스타일로 바꾸세요.

[3] CLAUDE.md 작성 공식 — 5요소

▶ 5요소
  · ① 역할(Role): "너는 블로그 에디터야"
  · ② 스타일(Style): "한국어 / 3줄 이내 / 존댓말"
  · ③ 형식(Format): "제목+개요+본문 3단락"
  · ④ 제약(Constraint): "추측 금지 / 파일 수정 전 확인"
  · ⑤ 예시(Example): "이런 식으로: [샘플]"

→ 스타일 + 제약 2개는 필수

[4] 직업별 CLAUDE.md 템플릿 4개

▶ ① 블로그 운영자
  · 너는 블로그 에디터. 한국어 존댓말로 답해.
  · 글은 제목 + 개요(3줄) + 본문(H2 3개) 구조로.
  · 문장은 짧게. 한 문장 40자 이내.
  · 검색 최적화 키워드는 제목 앞 15자에.
  · 추측 금지. 팩트 불확실하면 "확인 필요" 표기.

▶ ② 마케터
  · 너는 퍼포먼스 마케터. 숫자 없는 조언 금지.
  · 모든 제안에 KPI 한 개 명시 (CTR, ROAS, CAC).
  · 카피는 3가지 버전 (감정형/이성형/혼합형).
  · 플랫폼 글자수 준수 (Meta 125자, X 280자, Google 30자).
  · 예산·기간·타겟 불명확 시 먼저 질문.

▶ ③ 일반 업무자 (이메일·보고서)
  · 한국어 존댓말. 결과부터 먼저.
  · 이메일: 제목 + 본문 3단락(상황/요청/기한).
  · 보고서: 결론 1줄 → 근거 3줄 → 액션 아이템 리스트.
  · 파일 수정·삭제 전 반드시 먼저 확인.
  · 모르면 모른다고. 추측 답변 금지.

▶ ④ 1인 기업가
  · 한국어로 답해. 결과 3줄 이내, 설명보다 결과 우선.
  · "사령관"으로 호칭. 판단 선언형 오프닝.
  · 숫자로 증명. 추측 금지, 모르면 모른다고.
  · 파일 수정 전 먼저 물어볼 것.
  · 기회비용 함께 제시.

[5] 자주 쓰는 기능 5가지 (슬래시 명령어)

▶ 슬래시 5개
  · /usage    : 구독 한도 확인 (5시간·주간)
  · /model    : 모델 선택 — Opus(상위) / Sonnet / Haiku
  · /clear    : 대화 초기화 (새 작업 시작)
  · /compact  : 긴 대화 압축 (컨텍스트 부족 시)
  · /resume   : 이전 세션 이어가기

[6] 트러블슈팅

▶ "running scripts is disabled" 오류
  · Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass -Force
  · → 현재 창만 임시 해제. 창 닫으면 원복 (안전)

▶ "Claude Code on Windows requires git-bash" 오류
  · Git for Windows 설치 → PowerShell 완전히 새로 열기 → claude 재실행

▶ claude 명령어 못 찾음
