# Claude Opus 4.7 — 진짜 뭐가 달라졌나, 5분 정리

▶ 영상: https://youtu.be/d7hIYxXAb_E

---

※ [2] 스펙 비교 + [3] 벤치마크 비교는 본 메시지에 이어서 표 이미지 2장 첨부로 올립니다 (모바일에서 표 줄바꿈 깨짐 방지). 텍스트 요약은 아래 세로 나열본 참조.

[1] TL;DR — 일반 사용자 관점

▶ 핵심 3가지
  · 공개 모델 중 1위 탈환 (GPT-5, Gemini 3 제침)
  · 가격 동일 ($5 / $25 per Mtok) — 구독료·API 단가 변화 없음
  · Claude 구독자 자동 적용 — 별도 설정 불필요

→ 한 가지만 점검하세요: "내 프롬프트·CLAUDE.md가 모호하지 않나"
  4.7은 더 문자 그대로 해석합니다

[2] 스펙 비교 (4.6 → 4.7) — 세로 나열본

※ 원본 표는 별도 이미지 첨부

▶ 가격 — 동일
  · input: $5 / Mtok (변화 없음)
  · output: $25 / Mtok (변화 없음)

▶ 용량
  · 컨텍스트: 1M tokens (long-context 추가 요금 없음)
  · 최대 출력: 64k → 128k (2배)

▶ 이미지·토크나이저
  · 이미지 최대 해상도: 1568px / 1.15MP → 2576px / 3.75MP (3배+)
  · 토크나이저: 신규 (텍스트 토큰 1.0~1.35배 사용 가능)

▶ API model id
  · claude-opus-4-6 → claude-opus-4-7

[3] 벤치마크 비교 — 세로 나열본

※ 수치 출처: Anthropic 공식 발표 차트 (2026-04-16). 일부 차트 시각 판독. 원본 표는 별도 이미지 첨부

▶ SWE-bench Verified (실제 GitHub 오픈소스 버그 500개 수정)
  · 80.8 → 87.6  (+6.8%p ↑)

▶ CharXiv (논문 그래프·다이어그램 2천 장 해석)
  · 69 → 82  (+13%p ↑ — 최대 상승폭)

▶ BrowseComp (웹 검색·다단계 정보 조합)
  · 83.7 → 79.3  (−4.4%p ↓ — 유일 후퇴)

▶ CursorBench (코드 에이전트 평가)
  · 58% → 70%  (+12%p ↑)

▶ XBOW visual-acuity (시각 정밀도)
  · 54.5% → 98.5%  (+44%p ↑)

▶ CyberGym (사이버보안)
  · 4.7 기준 73.8 (4.6 갱신치)

▶ GDPval-AA / Finance Agent (지식 작업·금융)
  · SOTA 달성 (공개 모델 중 1위)

[4] 신기능 (전부 공식 출처 확인)

▶ xhigh effort level
  · 기존: low / medium / high / max
  · 4.7: 추가 권장 레벨 xhigh — 코딩·에이전트 작업 권장
  · Claude Code: xhigh 자동 적용 (사용자 설정 불필요)
  · Messages API에서만 노출. Managed Agents는 자동 처리

▶ /ultrareview (Claude Code 전용)
  · 작성 끝낸 코드를 별도 리뷰 세션으로 점검
  · 놓친 엣지 케이스·정리 포인트 사전 검출

▶ Task budgets (beta)
  · beta 헤더: task-budgets-2026-03-13
  · output_config에 task_budget: {"type": "tokens", "total": N}
  · 최소 20k tokens. 에이전트 루프 전체에서 모델이 자체 조절
  · max_tokens(하드 캡)와 다름 — task_budget은 모델 인지 advisory

▶ High-resolution image
  · 1568px → 2576px (1:1 픽셀 좌표 매핑 — scale-factor 계산 불필요)
  · 컴퓨터 사용·스크린샷·문서 분석에 직접 영향
  · 토큰 더 사용함 — 고해상도 불필요하면 사전 다운샘플 권장

▶ Auto mode (Max 사용자 확장)
  · 자율 의사결정 모드가 Max 플랜 사용자에게 확장

[5] Breaking Changes — API 사용자만 해당

※ Claude Managed Agents 사용자는 영향 없음. Messages API 직접 호출만 해당.

▶ Extended thinking budgets 제거
  · thinking: {budget_tokens: N} → 400 에러
  · thinking: {"type": "adaptive"}만 지원
  · adaptive thinking은 기본 OFF, 명시적으로 켜야 함

▶ Sampling 파라미터 제거
  · temperature, top_p, top_k 비기본값 → 400 에러
  · 프롬프팅으로만 동작 제어

▶ Thinking content 기본 omitted
  · 응답에 thinking field 비어 있음
  · 필요 시 display: "summarized" 명시

[6] Behavior Changes — 모든 사용자 (프롬프트 점검 필요)

▶ 명령을 더 문자 그대로 해석 (특히 낮은 effort에서)
  · 추측 안 함, 안 시킨 일 안 함

▶ 응답 길이 자동 조정
  · 작업 복잡도에 맞춰 유동적 (고정 verbosity 없음)

▶ 기본 도구 호출 감소
  · 추론 사용 ↑. effort 올리면 도구 사용 증가

▶ 톤 변화
  · 4.6의 따뜻한 검증조 → 더 직설적·의견 제시형
  · 이모지 축소

▶ 긴 에이전트 작업 진행 상황 업데이트 자주
  · 강제 status 메시지 scaffolding 제거 가능

▶ 기본 subagent 생성 감소

▶ 실시간 사이버보안 safeguard
  · 고위험 주제 거절 가능

→ 체크할 것: 자주 쓰는 프롬프트 / CLAUDE.md / 시스템 프롬프트에 "알아서 ~해줘" 류 모호한 표현 제거

[7] 가용성

▶ 이용 가능 채널
  · Claude.ai (Pro·Max)
  · Claude API
  · Amazon Bedrock
  · Google Cloud Vertex AI
  · Microsoft Foundry

▶ API model id: claude-opus-4-7

[8] 공식 1차 출처

▶ Anthropic 공식
  · 발표: https://www.anthropic.com/news/claude-opus-4-7
  · 모델 카드 (What's New): https://platform.claude.com/docs/en/about-claude/models/whats-new-claude-4-7

▶ 플랫폼 문서
  · Effort 가이드: https://platform.claude.com/docs/en/build-with-claude/effort
  · Adaptive Thinking: https://platform.claude.com/docs/en/build-with-claude/adaptive-thinking
  · Task Budgets: https://platform.claude.com/docs/en/build-with-claude/task-budgets
  · Migration Guide: https://platform.claude.com/docs/en/about-claude/models/migration-guide
