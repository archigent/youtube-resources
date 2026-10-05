# 감마 PPT 다 똑같죠 — 클로드 PPT, 강의·발표자료 Skill로 자동화

▶ 영상: https://youtu.be/0f7GQreyXkc

---

[1] lecture-slide Skill 다운로드

GitHub: https://github.com/archigent/lecture-slide
위 GitHub 링크에서 ZIP 다운로드


[2] 구성 파일

  · SKILL.md — 슬라이드 생성 원칙과 작업 순서
  · slide.html — 폰트, 색, 여백, 효과가 들어간 예시 템플릿
  · README.md — 설치와 수정 방법 안내


[3] 설치 (Claude Code · Codex 양쪽 지원)

  · Claude Code → ~/.claude/skills/lecture-slide/
  · Codex       → ~/.codex/skills/lecture-slide/

본인 쓰는 도구 폴더 한 쪽에 압축을 풀어 넣으면 됩니다.
위치가 헷갈리면 압축을 푼 뒤 대화창에 이렇게 요청해도 됩니다.

"이 폴더를 lecture-slide Skill로 쓰고 싶은데, 내 도구에 맞는 skills 폴더로 이동시켜줘."


[4] 한 줄 호출

"[주제] 강의·발표 자료 [N]장 만들어줘. 청중은 [페르소나]."

예시
  · 1인 사업가 시간 관리 강의안 8장 만들어줘. 청중은 외부 출강 수강생.
  · 사내 영업팀 대상 신규 CRM 발표자료 10장. 30대 영업 직원.
  · 신입 사원 온보딩 슬라이드 12장. 첫 출근 직후.


[5] 좋은 슬라이드 3대 룰 (Skill 안에 들어 있음)

  · 큼지막하게 — 제목 ≥ 64px, 본문 ≥ 40px
  · 한 페이지 한 메시지 — 두 가지 욱여넣지 X → 페이지 분리
  · 글자 양 적게 — 한 페이지 한국어 ≤ 6줄, 가장 긴 줄 ≤ 40자

룰이 깨지면 한 줄로 정정: "그 메시지는 다음 페이지로 분리해줘"


[6] 발표 모드 (생성된 HTML 파일 브라우저로 열기)

  · F11 — 풀스크린 진입
  · → / Space — 다음 슬라이드
  · ← — 이전 슬라이드
  · Ctrl+P → "PDF로 저장" — 회사 제출용


[7] 본인 톤 개조 (CSS 변수 한 줄 수정)

slides.html 상단:

  --accent: #2563eb;       /* 강조색 — 본인 회사 색으로 */
  --accent-deep: #1e3a8a;  /* 진한 강조 (표지 그래디언트) */
  --font-main: 'Paperlogy', 'Pretendard', sans-serif;
  --size-h1: 5.5rem;       /* 제목 사이즈 */
  --pad-x: 9%;             /* 좌우 여백 */

폰트는 원하는 거 다운받아 컴퓨터에 설치하면 자동 적용


[8] 톤 교체 예시

  · 블루 기본 — #2563eb / #1e3a8a / #dbeafe
  · 진한 녹색 (강의 톤) — #166534 / #14532d / #dcfce7
  · 보라 (창의 톤) — #7c3aed / #5b21b6 / #ede9fe
  · 다크 (시크) — #0f172a / #020617 / #cbd5e1
