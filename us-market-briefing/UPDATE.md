# 미국 증시 브리핑 동기화

현재 Work 브리핑을 GitHub Pages에 함께 게시합니다.

- 저장소: bestinvesting/bestinvesting.github.io, 브랜치 main
- 표시 페이지: /us-market-briefing/
- 데이터 파일: us-market-briefing/reports.json
- 원본: https://us-market-briefing-desk.bestinvestor.chatgpt.site/
- 연동 Site: appgprj_6af40ebd75fc819180645575af21dbdd

매일 Work 작업에서 원본 Site에 브리핑을 저장하고 검증한 후 read_market_briefings로 최신 기록을 읽습니다. GitHub fetch_file로 reports.json의 최신 내용과 blob SHA를 읽고 date를 키로 병합합니다. 기존 날짜는 유지하고 같은 날짜는 원본의 최신 값으로 갱신합니다. report.indices, issues.highlight, winners, losers, korea, watch 및 출처 URL을 그대로 보존합니다. GitHub update_file로 새 SHA를 적용하고 재조회하여 오늘 날짜·핵심 필드를 검증합니다. 충돌 시 최신 파일을 다시 읽어 병합하며 성공을 확인하기 전 완료를 보고하지 않습니다. 원본 저장과 GitHub 저장 성공 여부를 따로 기록합니다. 매일 HTML·블로그 테마를 수정할 필요는 없습니다. GitHub Pages 게시 완료까지는 추가 시간이 필요합니다.

개인 인증 정보나 API 키를 이 저장소에 저장하지 않습니다.

