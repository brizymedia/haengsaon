# 행사ON 홈페이지

정적 사이트 — GitHub Pages 로 배포: https://brizymedia.github.io/haengsaon/

제작: 큰길브리지 (주식회사 브리지미디어)

## 행사 준비 블로그 (2026-10-28, HD기획 _blog 루틴 이식)

- 주소 `blog/` — 글 원본 `_blog/posts/*.json`, 규칙 `_blog/GUIDE.md`(먼저 읽을 것), 지역 `_blog/regions.json`(= tools/make_pages.py AREAS), 사진 `_blog/photos.json`, 주제 `_blog/keywords.json`, 공식 출처 `_blog/sources.json`.
- 쓰기: `node scripts/blog-plan.mjs` → 글 JSON → `node scripts/blog-check.mjs --new <파일>` 통과 → `node scripts/build-blog.mjs`(blog/ · sitemap · llms.txt · rss.xml).
- 틀(머리글 · 메뉴 · 바닥글)은 notice.html 에서 빌린다. 메뉴를 바꾸면 notice.html 고치고 make_pages.py · build-blog.mjs 를 다시 돌린다.
- 글 안 주소는 사이트 루트 기준 `/…` 로 쓰고 빌드가 상대 주소로 바꾼다. 전용 도메인을 붙이면 build-blog.mjs 의 `SITE` 만 고친다.

## 업무 도구 (2026-10-03, 큰길이벤트기획 기능을 옮김 — 바로기획 기준본)

| 기능 | 주소 | 서버 |
|---|---|---|
| 자동 견적서(손님용) | `quote.html` | 문의 서버(공용) |
| 견적서 발행 · 저장함(관리자) | `quote.html?admin=1` | 저장함 폰·PC 같이 보기는 계약 서버 |
| 전자계약서 | `contract.html?admin=1` | 계약 서버(`apps-script/contract`) — 없으면 긴 서명 링크 |
| 거래명세서 | `statement.html?admin=1` | 없음 |
| 사진 올리기 + 블로그 · 인스타 글 만들기 | `upload.html` | 갤러리 서버(`apps-script/gallery`) → `photos` 가지 → 행사 사진 페이지 |
| 행사 이야기 | `stories/` | 없음 — `python tools/make_pages.py` |
| 운영 지역 | `areas/` | 없음 — 같은 명령 |
| 문의 알림 | `contact.html` 폼 · 가격표 요청서 · 견적서 | 문의 서버 → 대표 메일 + 큰길브리지 |
| 행사 일정 · 체크리스트 | `schedule.html` | 계약 서버(일정 기능 — 스크립트 속성 `CREW_PW` 필요) |
| 대표 전용 업무 문서함 | `office.html` | 없음 — 도구 모음 · 서버 연결 상태 · 암호 안내(noindex) |
| 유입 현황 · AI 검색 | `stats.js` · `llms.txt` · `sitemap.xml` · `robots.txt` | 큰길브리지 유입 서버 |

- 서류 3종 · `upload.html` · `schedule.html` · `quote-catalog.js` · 서버 코드 · `office.html` 은 큰길이벤트 원본에서 `python tools/port_docs.py` 로 옮긴다(원본이 바뀌면 다시 돌리면 됨). 손수정은 그 스크립트의 「회사 설정」 칸에.
- 견적서 품목표는 가격표(`price.html`) 8분류 32품목 그대로, 금액은 비워 둠(`price:null`).
- 직인: `assets/img/stamp-haengsaon.png` (투명 PNG) 가 생기면 계약서 · 명세서에 찍힌다. 없으면 「(인)」 자리만.
- 계약 · 사진 서버는 아직 배포 전. 배포하면 `tools/port_docs.py` 의 `CONTRACT_URL` · `GALLERY_URL` 에 넣고 다시 돌린다.
- `office.html` · `schedule.html` 은 공개 메뉴에 링크하지 않는다.
