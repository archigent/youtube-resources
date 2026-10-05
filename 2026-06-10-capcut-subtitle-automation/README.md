# 캡컷 자막 자동화, 2시간을 15분으로 줄였습니다

▶ 영상: https://youtu.be/qn_mY4i8xh8

---

[1] srt-subtitle Skill 다운로드

GitHub: https://github.com/archigent/srt-subtitle
위 GitHub 링크에서 ZIP 다운로드


[2] 구성 파일

  · SKILL.md — 자막 생성 원칙과 작업 순서
  · README.md — 설치와 수정 방법 안내


[3] 설치 (Claude Code · Codex 양쪽 지원)

  · Claude Code → ~/.claude/skills/srt-subtitle/
  · Codex       → ~/.codex/skills/srt-subtitle/

  압축을 풀어 한 쪽에 넣으세요. 자막 엔진 whisperx도 한 번 설치합니다:
  · pip install whisperx   (+ ffmpeg)


[4] 한 줄 호출

  "이 영상 자막 만들어줘"  /  "자막 뽑아줘"

  → whisperx로 단어 타임스탬프 추출 → 의미 단위 분할 → 캡컷 임포트용 .srt 출력.
  GPU 약하면 large-v3 대신 large-v3-turbo / medium / small. CPU도 가능합니다.


[5] 쓸 때 팁

  · 의미 단위로 끊고 조사·고유명사는 마지막에 한 번 눈으로 확인
  · 한 줄 28자 안쪽이 읽기 편함
