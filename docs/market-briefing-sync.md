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


## 2026-11-14 통합 메뉴 · 최신 지침
이전의 미국·크립토 두 개만 표시 규칙을 대체한다. 상단 메뉴는 미국 증시(`/`), 한국 주식시장(`/korea-market-briefing/`), 크립토 시장(`/crypto-market-briefing/`), 토론의 장(`/forum/`) 네 개다. 첫 화면은 미국 증시 브리핑으로 유지. 기존 메뉴 링크를 다시 노출하지 않으며 `/blog/` 직접 접근은 보존한다. 한국 페이지 정식 제목은 한국 주식시장 브리핑. 향후 개별종목은 미국 종목 분석/한국 종목 분석으로 분리하며 미구현 메뉴를 추가하지 않는다.
- 한국·토론은 현재 서비스 준비 중인 공개 시안. 가상 데이터·예시 글·AI 요약 예시임을 표시한다. 로컬 체험은 각 브라우저에만 저장한다. 시안을 실제 시황/공동 게시로 재표기하지 않는다.
- 한국 상단: KOSPI, KOSDAQ, USDKRW, 국고채3년, vKOSPI, 기관 현물(유가증권시장·억원), 외국인 선물(계약). KOSPI200 지수·외국인 현물 카드는 제외.
- 코스피 상승/하락, 코스닥 상승/하락 테마는 별도 4영역, 기본 각3개이나 유의미한 테마 수에 따라 가변.
- assets/korea-forum.js와 css를 두 페이지가 공유하며, 기존 Site 복사본으로 새 페이지를 덮어쓰지 않는다. 공통 네비게이션과 방문 카운터를 보존한다.
- 실제 공동 게시와 구글/GitHub 인증, 비로그인 관리 비밀번호, 관리자 숨김/복원/휴지통/잠금, AI 요약은 아직 미연결. 비밀번호·계정 정보를 정적 HTML/JS/localStorage에 저장하지 않는다. 관리자 권한을 클라이언트 변수만으로 구현하지 않는다.
