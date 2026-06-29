# semas-scrape-test

Claude Code 클라우드 루틴 환경에서 Firecrawl MCP로 외부 사이트 스크래핑이 가능한지 검증하는 테스트 프로젝트.

## 테스트 대상

| 사이트 | URL | 스크래핑 방식 |
|--------|-----|--------------|
| 소상공인시장진흥공단 | https://www.semas.or.kr/web/board/webBoardList.kmdc?bCd=2001&pNm=BOA0101 | 기본 |
| K-Startup 창업지원포털 | https://www.k-startup.go.kr/web/contents/bizpbanc-ongoing.do | stealth 프록시 + JS 렌더링 |

## 아키텍처

메인 에이전트가 각 사이트별 서브에이전트를 병렬 실행:
- 서브에이전트 A → 소상공인시장진흥공단
- 서브에이전트 B → K-Startup 창업지원포털

## 결과 확인

루틴 실행 후 `output/` 디렉토리 확인:
- `result.md` — 스크래핑 결과 (사이트별 섹션)
- `log.md` — 성공/실패 로그
