# Semas Scrape Test — 루틴 지침

## 목적
이 루틴은 Firecrawl MCP가 클라우드 루틴 환경에서 외부 웹사이트를 스크래핑할 수 있는지 테스트한다.

## 실행 지침

1. Firecrawl MCP의 `firecrawl_scrape` 도구를 사용해 아래 URL을 스크래핑하라:
   - URL: `https://www.semas.or.kr/web/board/webBoardList.kmdc?bCd=2001&pNm=BOA0101`
   - 옵션: `formats: ["markdown"]`

2. 결과를 `output/result.md`에 저장하라. 내용 예시:
   - 스크래핑 성공 시: 추출된 공지 목록 마크다운
   - 실패 시: 에러 메시지 전문

3. `output/log.md`에 실행 로그를 기록하라:
   - 실행 시각 (UTC)
   - 성공/실패 여부
   - 사용한 도구명
   - 에러 코드 및 메시지 (실패 시)
   - 응답 소요 시간 (가능하면)

4. `output/` 디렉토리의 변경사항을 커밋하고 푸시하라:
   - 커밋 메시지: `test: scrape run [성공/실패] YYYY-MM-DD`

## 주의
- API key 없이 Firecrawl 도구 호출이 실패하면 그 에러도 log.md에 기록할 것
- 절대 루틴을 중단하지 말고, 실패해도 log.md 커밋까지는 완료할 것
