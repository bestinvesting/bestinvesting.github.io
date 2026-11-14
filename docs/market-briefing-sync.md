# Market briefing publishing

- `/` is the US market briefing. It uses the same absolute `/us-market-briefing/reports.json` and `/us-market-briefing/regime-reports.json` paths as the original briefing URL.
- `/crypto-market-briefing/` is the native GitHub Pages crypto briefing and narrative report. It reads only same-origin JSON; no private Site tokens are shipped to visitors.
- `/blog/` preserves the original GitBook home, with its existing lecture/post menus. `README.md` owns that permalink.
- Shared navigation is `assets/market-navigation.js`. Preserve this include during any HTML update.

After each successful crypto Site publication, the linked 07:30 KST cloud task must read back both complete lists from the owned Site using supported service access and mirror non-demo records to:

1. `crypto-market-briefing/data/reports.json`
2. `crypto-market-briefing/data/insights.json`
3. Date snapshots under `crypto-market-briefing/data/daily/YYYY-MM-DD.json` and `data/reports/YYYY-MM-DD.json`.

Use authenticated GitHub tools for repository `bestinvesting/bestinvesting.github.io`, branch `main`. Read the current ref and commit tree; build an additive tree over the current tree; commit all changed JSON together; update the ref with expected_sha and no force. On a concurrent change, fetch the new head, preserve unrelated edits, and retry the merge. Preserve every earlier date; do not replace a full list with only today's entry. Git commit history preserves same-day revisions.

Do not copy access tokens, private operational instructions, or user account information. Public market report content is authorized for this public blog. If either publication fails, state which destination succeeded and which failed. A GitHub commit is not proof that Pages deployment succeeded; check the deployment workflow status.

The US update task continues to update `us-market-briefing/reports.json` and regime records. The homepage reads those same files, so it updates together without duplicating data. Preserve the shared menu script and absolute data routes if refreshing briefing HTML.


## 김치 프리미엄 · 방문 집계 (2026-11-14)
- 데일리 metrics에 김치 프리미엄을 포함한다. 국내 BTC KRW / (해외 BTC USD × USDKRW) - 1. 양쪽 가격 시각과 환율 기준일을 기록한다. 주말 기준환율 사용은 참고값으로 명시. 전일 동일 기준이 없으면 전일비를 만들지 않는다. 본문에는 의미 있는 변화만 반영한다.
- 상단 7개 카드 및 전일 비교를 유지한다. 과거 미관측 값은 —로 표시한다.
- assets/market-navigation.js는 하단 익명 브라우저 방문 집계를 실행한다. 집계 API는 공개 미국 Site의 /api/visitors이며 보고서 저장 권한과 독립적이다. 날짜는 KST, 누적은 전체 고유 브라우저, 오늘은 당일 고유 브라우저. 집계 시작 2026-11-14, IP 미저장. 삭제·덮어쓰기 금지. 오류시 숨긴다.


## 표시 유지 (2026-11-14 추가 수정)
- 크립토 상단 7개 지표는 PC(801px 이상)에서 한 줄로 표시한다. 시장 리포트에도 동일하게 적용한다. 800px 이하에서는 미국 브리핑과 같이 2열로 표시한다.
- GitHub 미국 브리핑의 원본 브리핑 링크는 제거된 상태를 유지한다. 원문 뉴스·통계 출처 링크는 보존한다.
