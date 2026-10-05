# 뉴스 확인 1시간, AI로 5분까지 줄였습니다

▶ 영상: https://youtu.be/Qlrtcw6YNzc

---

[1] 한 줄 요약

▶ 매일 아침 본인 관심 분야 뉴스 자동 브리핑 시스템 (영상에서 시연한 실 운영 그대로)
· RSS로 그날 새 기사 수집 (본인 관심 분야 6개 카테고리)
· LLM이 한국어 3줄 요약 + 분야별 분류
· Discord로 매일 자동 알림 (출근길 폰 5분 훑기용)
· Google Sheets에 매일 누적 (Claude Code 토론 사이클용)
· GitHub Actions가 매일 8시 자동 실행
→ 매일 1시간 → 본인 분야 5분 + 매일 자료 누적 자산

[2] Skill 다운로드 (직접 만들지 마시고)

▶ 위치
· GitHub: https://github.com/archigent/cc-07-news-brief
· Code 버튼 → Download ZIP

▶ 설치
· 압축 풀기
· ~/.claude/skills/ 폴더에 복사 (Codex는 ~/.codex/skills/)
· 폴더 없으면 새로 만들기

▶ 한 마디 셋업
Claude Code 또는 Codex 열고:
"이 skill로 [본인 분야] 셋업해줘. 카테고리는 [6개 콤마 구분]로.
LLM 키 X, Discord webhook Y, credentials.json은 Z, 시트 ID는 W."

예시 — 투자: 주식·부동산·코인·매크로·글로벌·정책
예시 — 연예: K팝·드라마·영화·셀럽·예능·해외엔터
예시 — 비즈니스: AI·스타트업·마케팅·매출·트렌드·리더십

[3] 사전 발급 키 4개 (총 6분)

▶ LLM API 키 (무료)
· 오픈라우터: https://openrouter.ai/keys (Sign in → Create Key)
· 또는 제미나이 무료 키: https://aistudio.google.com/apikey
· 매일 60개 기사면 무료 한도 안

▶ Discord 웹후크 (1분)
· 본인 디스코드 서버 → 채널 우클릭 → Edit Channel
· Integrations → Webhooks → New Webhook → Copy URL

▶ Google Service Account credentials.json (3분)
· console.cloud.google.com → 신규 프로젝트
· API 및 서비스 → Google Sheets API 사용 설정
· 사용자 인증 정보 만들기 → 서비스 계정 → 만들기
· 서비스 계정 → 키 탭 → 키 추가 → JSON → 다운로드 → credentials.json 저장

▶ Google Sheets ID + 권한 공유 (1분)
· sheets.google.com → 새 시트 생성
· URL docs.google.com/spreadsheets/d/[ID]/edit 에서 ID 복사
· 시트 우상단 공유 → credentials.json의 client_email에 편집자 권한 (필수)

▶ GitHub 저장소 + Secrets 4개 (1분)
· GitHub 새 저장소 만들고 skill 파일 푸시
· 저장소 Settings → Secrets and variables → Actions → New
· 등록 4건:
· LLM_API_KEY = LLM API 키
· DISCORD_WEBHOOK_URL = Discord webhook URL
· GOOGLE_CREDENTIALS = credentials.json 파일 내용 JSON 그대로
· SPREADSHEET_ID = Sheets URL의 ID

[4] 매일 사용 흐름

▶ 매일 아침 8시 — 자동 발송
· 본인 PC 꺼져 있어도 깃허브 서버가 자동 실행
· 영국 시각 기준이라 한국 8시 = UTC 23시 (전날) 변환 자동

▶ Discord 채널에 도착 — 출근길 폰 5분
· 카테고리별 색상 알림 (정치 빨강·경제 초록·기술 파랑 등)
· 각 기사 = 제목 + 한국어 3줄 요약 + 원문 링크 + 출처
· 본인 분야만 추려서 보기 (다른 분야 스킵)

▶ Google Sheets에 매일 누적 — 사무실 Claude Code 토론
· 전체 기사 + 본문 + 한국어 3줄 요약 매일 행 추가
· Claude Code 한 마디:
· "오늘 시트 가져와서 본인 분야 핵심 짚어줘"
· "이번 주 시트에서 트렌드 3가지 뽑아줘"
· "이번 달 [카테고리] 누적 흐름 분석해줘"
· 매일 자료 누적 = 본인 영역 인사이트 자산

[5] 왜 MCP가 아니라 Service Account?

▶ Google Sheets MCP도 있지만 — MCP는 Claude Code를 켜고 대화하는 중에만 작동
▶ 본 skill은 본인 PC 꺼져 있어도 매일 8시 GitHub Actions가 자동으로 시트 채우는 게 본질
▶ 그래서 Claude Code 의존도 0인 Service Account 방식 (credentials.json 파일 인증)
▶ 한 번 셋업해두면 매일 자동 누적 + 토론 둘 다 가능

[6] 트러블슈팅

▶ 기사 0건 수집
· RSS 주소가 잘못. Claude에 "사이트 RSS 다시 찾아줘"

▶ LLM 응답 401
· API 키 잘못 또는 만료. .env 확인

▶ LLM rate limit (429)
· 요청 간격 sleep 값을 0.5 → 1.0으로 증가

▶ Discord 메시지 안 옴
· webhook URL 잘못 또는 채널 권한 확인

▶ Sheets 권한 에러
· Service Account 이메일을 시트 공유 편집자에 추가 안 함
· credentials.json client_email 확인 후 시트 공유 부여

▶ Sheets 행 추가 안 됨
· GOOGLE_CREDENTIALS JSON 형식 오류
· GitHub Secrets에 credentials.json 파일 내용 그대로 붙여넣었는지 확인

▶ GitHub Actions 실행 안 됨
· cron 시간이 UTC인지 확인
· 저장소 Actions 탭에서 수동 실행 (Run workflow) 테스트
