# KOSPI200 Weekly / Daily Report publishing

두 종류 모두 한국 주식시장 브리핑 > 시장리포트에 게시한다. 기존 07:30 한국 데일리 시황 및 미국·크립토·토론은 별도이며 변경하지 않는다.

## Content and dates
- Weekly: 제목 KOSPI200 Weekly Report — YYYY년 M월 D일, 일요일 주간호 날짜, reportType weekly, id kospi200-weekly-YYYY-MM-DD. 최근 완료된 한국·미국 거래주 기준 심층 분석과 다음 주 검증 과제.
- Daily: 제목 KOSPI200 Daily Report — YYYY년 M월 D일, 한국 당일 거래일 날짜, reportType daily, id kospi200-daily-YYYY-MM-DD. 2~3분 분량: 핵심 변화 3개 → 갭·장초/오후·변동성·종가·옵션헤지 확인 조건 → 직전 가설 유지/수정/보류 → 이벤트 2~3개. 사실/추론/실험 가설을 구분한다.
- Daily는 한국 거래소가 실제 개장하는 날만 게시한다. 주말, 공휴일, 근로자의날, 연말휴장, 임시휴장을 KRX 공지·휴장 캘린더로 확인하고 휴장일은 새 글·알림 없이 SKIP_COMPLETION. 수능일 개장 지연은 휴장이 아니며 실제 거래시간을 표시한다. 거래일 확인이 막히면 임의로 발행하지 말고 확인 불가를 보고한다.
- 오전 06:00 시점 미국 정규장 종가가 막 형성되거나 검증 전일 수 있다. 최신 확인 장중·잠정 관측은 그 시각과 상태를 명시하고 종가로 둔갑시키지 않는다. 향후 발표될 NVIDIA 실적 등은 미발표로 표시한다.
- 모든 수치는 실제 날짜·시각·단위와 동작하는 원문 URL. 한국 전일 종가와 당일 장전값, 현물/선물 비동시점 종가차, 외국인 선물 금액/계약을 구분한다. 미확인 데이터는 미확인. 통계로 보정하지 않은 전망확률·OI만으로 딜러 방향·임의 매매가를 만들지 않는다.
- originalBody와 실제 originalCreatedAt/publishedAt은 보존한다. 정정은 updatedAt/correctionReason, 이전 id는 previousId. 주간호 날짜를 옮겨도 실제 작성시각이나 asOf를 과거로 조작하지 않는다.

## Storage and merge
GitHub repository bestinvesting/bestinvesting.github.io main:
- korea-market-briefing/data/market-reports.json (전체 배열, reportType+id로 기존 모든 레코드 병합)
- korea-market-briefing/data/market-reports/YYYY-MM-DD.json (해당 보고서 스냅샷)
Schema: id,reportType,date,title,summary,asOf,publishedAt,originalCreatedAt,notice,sources[{title,url,asOf}],body(Markdown),originalBody.
현재 ref와 commit tree를 읽고 base tree 위에 관련 JSON만 변경해 커밋한다. expected_sha, force=false. 충돌 시 최신 main에 재병합한다. 예전 날짜 스냅샷은 감사이력으로 보존하되 목록에는 정정본만 표시한다. source renderer, 메뉴, 일일 reports.json, 포럼을 덮어쓰지 않는다.
GitHub actions/runs?head_sha=커밋으로 Pages build and deployment 성공을 확인한다. PR 전용 workflow 도구만으로 main 배포를 판단하지 않는다. 공개 JSON을 재조회한다.

원본 한국 Site project appgprj_6af837385228819185cf105cade02c7a:
get_site로 현재 URL·audience를 확인하고 Sites skill의 supported source workflow로 최신 소스를 연다. dist/korea-market-briefing/data/market-reports.json과 dist/korea-market-briefing/data/market-reports/YYYY-MM-DD.json에 동일한 병합본을 저장한다. JSON과 JS 검증 뒤 소스 push·archive·기존 audience로 배포한다. 정적 Site이므로 source publication이 필요하며 API 저장 경로를 발명하지 않는다. GitBlog·Site 최신 이력을 합쳐 동시 작업으로 기존 글이 유실되지 않도록 한다. credentials는 메모리/stdin에만 유지하고 파일·출력·커밋에 남기지 않는다.
현재 Site는 owner-only이며 유지한다. 읽기 벽을 우회하거나 임의 공개하지 않는다. Site native 배포 성공 및 게시 데이터 동일성을 확인한다.
두 목적지 중 하나가 실패하면 성공한 쪽과 실패한 쪽을 분리해 보고하며 둘 다 확인 전 전체 완료라고 하지 않는다. 실패 때문에 반복 예약을 임의 해제하지 않는다.
Links: https://korea-market-forum-review.bestinvestor.chatgpt.site/?tab=report 및 https://bestinvesting.github.io/korea-market-briefing/?tab=report
