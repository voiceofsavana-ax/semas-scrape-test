# Multi-Site Scrape — 루틴 지침

## 목적

이 루틴은 Firecrawl MCP를 사용해 두 개의 창업지원 사이트를 **서브에이전트로 병렬 스크래핑**하고 결과를 output/에 저장한다.

## 스크래핑 대상

| 사이트 | URL | 비고 |
|--------|-----|------|
| 소상공인시장진흥공단 | https://www.semas.or.kr/web/board/webBoardList.kmdc?bCd=2001&pNm=BOA0101 | 기본 스크래핑 |
| K-Startup 창업지원포털 | https://www.k-startup.go.kr/web/contents/bizpbanc-ongoing.do | stealth 프록시 + JS 렌더링 |

## 실행 지침

아래 두 서브에이전트를 **병렬**로 실행하라:

### 서브에이전트 A — 소상공인시장진흥공단

`firecrawl_scrape` 도구로 스크래핑:
- URL: `https://www.semas.or.kr/web/board/webBoardList.kmdc?bCd=2001&pNm=BOA0101`
- 옵션: `formats: ["markdown"]`, `onlyMainContent: true`
- 스크래핑 결과 전문을 리턴하라

### 서브에이전트 B — K-Startup 창업지원포털

`firecrawl_scrape` 도구로 스크래핑:
- URL: `https://www.k-startup.go.kr/web/contents/bizpbanc-ongoing.do`
- 옵션: `formats: ["markdown"]`, `onlyMainContent: true`, `proxy: "stealth"`, `waitFor: 5000`
- 스크래핑 결과 전문을 리턴하라

### 취합 및 저장

두 서브에이전트 결과를 모아 아래 순서로 처리하라:

1. **`output/result.md` 저장** — 형식:
   ```
   # 창업지원 공고 수집 결과
   수집일시: YYYY-MM-DD HH:MM UTC

   ## 소상공인시장진흥공단
   [서브에이전트 A 결과]

   ## K-Startup 창업지원포털
   [서브에이전트 B 결과]
   ```

2. **`output/log.md` 기록** — 포함 항목:
   - 실행 시각 (UTC)
   - 각 사이트별 성공/실패 여부
   - 에러 코드 및 메시지 (실패 시)
   - 사용한 proxy 옵션

3. **`output/` 커밋 & 푸시**:
   - 커밋 메시지: `test: scrape run [성공/실패] YYYY-MM-DD`

## 주의

- 서브에이전트 중 하나가 실패해도 나머지 결과는 반드시 저장할 것
- 실패해도 log.md 커밋까지는 반드시 완료할 것
- Firecrawl API key 오류 시 에러 전문을 log.md에 기록할 것
