# CLAUDE.md: TOPIK Practice Bank 인수인계서

작성일: 2026-10-07 (claude.ai 대화에서 Claude Code로 인계)

## 1. 프로젝트 한 줄 요약

외국인 TOPIK 수험생을 대상으로, 무료 유형 분석 글과 미니 테스트로 유입을 만들고 **직접 창작한** 유료 문제은행·모의고사 PDF를 Gumroad로 판매하는 영어 중심 정적 블로그.

## 2. 현재 상태

| 항목 | 상태 |
| --- | --- |
| GitHub 계정 | `wq54696-dotcom` (가입·로그인 완료) |
| 저장소 | `wq54696-dotcom/topik-bank`, Public. 로컬 원본: `Desktop\topik_bank\topik-bank` (git 저장소) |
| 사이트 파일 | 첫 커밋 푸시 완료 (2026-10-07) |
| GitHub Pages | 켜짐, 빌드 성공. https://wq54696-dotcom.github.io/topik-bank/ |
| 푸시 방법 | 터미널 git에는 GitHub 인증 없음. 커밋은 Claude가, 푸시는 GitHub Desktop에서 사용자가 |
| 로컬 빌드 검증 | 안 됨 (Ruby 미설치). GitHub Pages 빌드로 확인 |
| 사용 안 하는 저장소 | `topik-bank-Public` (빈 저장소, 삭제 예정) |
| 도메인, Gumroad, giscus, 분석 | 전부 미설정 (설정값은 빈칸 또는 예시값) |
| 사용 도구 | Windows PC, GitHub Desktop 사용 중 |

## 3. 바로 할 일 (순서대로)

> 1~4번 완료 (2026-10-07). 글 주소는 `/lessons/:title/` (파일명의 슬러그 기준), 카테고리 아카이브도 `/lessons/`.

1. 이 폴더 내용을 저장소에 커밋하고 푸시
   - 커밋 메시지 예: `Initial site skeleton (Jekyll + Minimal Mistakes)`
2. GitHub 저장소 Settings → Pages: Source `Deploy from a branch`, Branch `main`, `/ (root)`
3. Actions 탭에서 빌드 성공 확인, `https://wq54696-dotcom.github.io/topik-bank/` 접속 확인
4. 빌드 실패 시 로그의 파일·줄 번호 기준으로 수정 (가장 흔한 원인: 머리말 YAML, `remote_theme` 버전, Liquid 문법)
5. `_config.yml`의 "바꾸세요" 항목을 사용자에게 물어 채우기: `title`, `author.name`, `author.bio`, Gumroad 주소 3곳, `repository`는 `wq54696-dotcom/topik-bank`로 이미 알 수 있으니 바로 수정
6. 로컬 미리보기 환경 구성 (선택): Ruby + `bundle install` + `bundle exec jekyll serve`. Windows라면 RubyInstaller(Devkit 포함) 필요

## 4. 기술 구성

- 정적 사이트: Jekyll, GitHub Pages 기본 빌드 (`github-pages` gem 기준). 도메인 구매 시 Cloudflare Pages로 이전 예정 (8번 로드맵)
- 테마: `remote_theme: mmistakes/minimal-mistakes@4.26.2`
- `baseurl: "/topik-bank"` (개인 도메인 연결 후 `""`로 변경, `url`도 함께 수정)
- 한글 폰트: `_includes/head/custom.html`에서 Noto Sans KR 로드, `assets/css/main.scss`에서 `$sans-serif` 덮어씀
- 컬렉션 `shop`: `_shop/*.md` → `/shop/:name/`
- 댓글: giscus 설정 자리만 있음 (`repo_id`, `category_id` 비어 있음)

## 5. 폴더 구조와 규칙

| 위치 | 용도 | 규칙 |
| --- | --- | --- |
| `_posts/` | 유형 분석 글 | 파일명 `YYYY-MM-DD-english-slug.md`, 카테고리는 아래 목록 중 하나 |
| `_shop/` | 상품 상세 페이지 | 머리말에 `price`, `gumroad_url`, `header.teaser` |
| `_pages/` | home, lessons, free, shop, about, subscribe | 각 파일에 `permalink` 지정 |
| `_includes/product-box.html` | 글 하단 상품 추천 박스 | `{% include product-box.html title="" desc="" url="" %}` |
| `assets/free/` | **무료** PDF만 | 유료 파일 절대 금지(공개 저장소라 누구나 받을 수 있음) |
| `assets/images/` | 표지, 샘플 페이지 이미지 | 장당 300KB 이하, `sample-cover.png`는 임시 표지 |
| `_data/navigation.yml` | 상단 메뉴 | |
| `README.md` | 사용자용 한국어 운영 안내 | 사이트 빌드에서 제외됨 |

| `_drafts/` | 검수 전 글 초안 | 사이트에 안 나옴(저장소에는 공개). 검수 후 날짜 붙여 `_posts/`로 이동 |

저장소 밖 파일 (`Desktop\topik_bank\`, 공개 금지):
- `문항관리.xlsx`: 시트 `현황`(자동 집계) / `문항` / `목록`(드롭다운 값) / `유형표`(번호 구간, topik.go.kr 대조 전 "확인 필요"). 행 추가는 Excel COM으로. openpyxl로 저장하면 시트 간 드롭다운이 지워짐
- 유료 상품 원고·PDF도 여기 둠

카테고리(통일해서 사용): `TOPIK I Reading`, `TOPIK I Listening`, `TOPIK II Reading`, `TOPIK II Listening`, `TOPIK II Writing`, `Vocabulary & Grammar`, `Exam Guide`

파일 크기: 1개 50MB 미만 유지(100MB 초과 업로드 불가). 큰 무료 PDF는 GitHub Releases로.

## 6. 콘텐츠 원칙 (가장 중요)

**저작권**
- TOPIK 기출문제는 저작물. 원문 복사, 숫자·단어만 바꾼 변형 문제 판매 금지
- 문항 **유형**(빈칸, 중심 생각, 순서 배열 등)은 참고 가능. 지문·대화·보기·정답 해설은 전부 새로 작성
- 신문 기사, 소설, 광고 문구 등 타인의 글을 지문에 넣지 않음. 기사 활용 시: 사실만 목록으로 추출 → 원문을 보지 않고 새 구성으로 작성 → 여러 출처 혼합. 원문과 문단 순서가 같거나 3어절 이상 같은 구절이 반복되면 다시 쓰기
- AI 초안을 그대로 쓰지 말고 사람이 수정·해설을 더해 창작 기여를 분명히 할 것
- 이미지·폰트는 상업적 이용 가능한 것만
- 사이트는 NIIED(국립국제교육원)와 무관하다는 문구 유지 (`_pages/about.md`)

**글 구성**
- 설명은 영어, 문제는 실제 시험처럼 한국어
- 유형 분석 글 구조: 유형 소개 → 풀이 방법 → 연습 문제 2~5개 → 접을 수 있는 정답·해설(`<details>`) → 관련 상품 박스
- 제목은 학습자가 실제 검색하는 영어 문장으로, `excerpt` 1~2문장 필수

**TOPIK 시험 구성 (PBT, 문제 제작 기준)**

| 시험 | 영역 | 문항 | 시간 |
| --- | --- | --- | --- |
| TOPIK I | 듣기 / 읽기 | 30 / 40 | 40분 / 60분 |
| TOPIK II | 듣기 / 쓰기 / 읽기 | 50 / 4 (51~54번) / 50 | 60분 / 50분 / 70분 |

IBT는 문항 수가 적고 시간이 짧음. 제작 전 topik.go.kr에서 최신 기준 확인.

## 7. 판매 구조

- 결제·파일 전달: Gumroad (국내 은행 원화 정산 지원, 10% + $0.50 수수료)
- 상품 라인업과 제안 가격(USD): 무료 미니 테스트 $0(이메일) / 유형별 문제은행 30제 $4~7 / 쓰기 51~54번 자료 $7~12 / 실전 모의고사 1회 $8~15 / 묶음 단품 합계의 70%
- 구매 버튼: 상품 상세 페이지 상단·하단, 레슨 글 하단 박스, 홈 배너
- 문항 관리: 스프레드시트 필드 `문항 ID(T2-R-16-0007) / 시험·영역 / 대응 번호·유형 / 난이도 / 지문·보기 / 정답·영어 해설 / 사용처`

## 8. 남은 로드맵

1. 사이트 뼈대 공개 (위 3번 항목)
2. 콘텐츠: 문항 관리 스프레드시트, 유형 분석 글 10편(TOPIK I 4, II 6), 무료 미니 테스트 2종, 첫 유료 상품 1종(유형별 30제), 샘플 이미지
   - 완료: 문항관리.xlsx (27문항: 공개 2, 초안 25) / 글 공개 1편(T2 읽기 빈칸)
   - 초안 9편(`_drafts`, 사용자 검수 대기): TOPIK I 읽기 31~33 주제어, 34~39 빈칸, 40~42 실용문 불일치, 46~48 중심 생각 / TOPIK II 읽기 13~15 순서 배열, 25~27 신문 기사 제목 / 쓰기 51~52, 53 그래프, 54 에세이
   - 유형 분석 글 10편 목표 달성 (공개 1 + 초안 9). 듣기 글은 음성 파일 필요해 보류
   - 다음: 무료 미니 테스트 2종(PDF), 첫 유료 상품(T2 읽기 빈칸 30제) 원고, 샘플 이미지
   - 쓰기 모범 답안 글자 수: 53번 238자, 54번 약 660자 (공백 포함, 문단 들여쓰기 1칸씩 포함)
   - 다음 유료 상품 후보: TOPIK II 쓰기 51~54 자료 ($7~12). 쓰기 초안 글의 상품 박스는 현재 `/subscribe/`로 연결("coming soon")
3. 판매 연결: Gumroad 가입·은행 연결, 상품 등록, 구독자 할인 코드, 상품 페이지 링크 교체, giscus·분석 연결
4. 공개·유입: 개인 도메인 연결 + Cloudflare Pages 이전(아래), Search Console 사이트맵 제출, Reddit·Pinterest 등에 무료 자료 공유, 주 1~2편 발행

### 개인 도메인 `topikbank.com` + Cloudflare Pages 이전 (결정됨, 구매 대기)

**왜 옮기나**: GitHub Pages 규정은 "주로 상거래를 위한 사이트"를 금지. 결제는 Gumroad라 지금은 괜찮지만, 상품이 늘면 위반 소지. Cloudflare Pages는 무료 요금제에서도 상업적 이용 허용. 주소가 어차피 바뀌는 도메인 연결 시점에 함께 옮김. **유료 상품 본격 판매 전에 완료할 것.**

**그때까지**: GitHub Pages 유지. 학습 글 중심, 판매 링크는 보조로.

도메인: 2026-10-07 RDAP 조회 시 미등록. 영구 구매 불가(최대 10년 선결제), 1~2년 + 자동 갱신 권장.

1. [사용자] Cloudflare 가입 → Domain Registration에서 `topikbank.com` 구매 (원가 판매, WHOIS 개인정보 기본 보호, 자동 갱신 확인). DNS도 Cloudflare에서 자동 관리됨
2. [사용자] Workers & Pages → Create → Pages → Connect to Git → `wq54696-dotcom/topik-bank` 선택 (GitHub 연동 권한 승인 필요)
3. [Claude 안내] 빌드 설정: Framework `Jekyll`, Build command `bundle exec jekyll build --baseurl ""`, Output `_site`, 환경 변수 `RUBY_VERSION` (Gemfile의 github-pages gem과 맞는 버전, 이전 시 확인). `--baseurl ""` 덕분에 `_config.yml`을 안 바꿔도 GitHub Pages와 동시에 작동
4. [Claude] `*.pages.dev` 임시 주소에서 전 페이지 점검 (홈, 레슨, 상품, CSS, 한글 폰트)
5. [사용자] Pages 프로젝트 → Custom domains → `topikbank.com`, `www.topikbank.com` 추가 (같은 Cloudflare 계정이라 DNS 레코드 자동 생성, HTTPS 자동)
6. [Claude] `_config.yml`: `url: "https://topikbank.com"`, `baseurl: ""`로 수정 커밋 → 빌드 명령의 `--baseurl ""`는 그대로 둬도 무방
7. [사용자] GitHub 저장소 Settings → Pages 끄기 (Unpublish). 예전 github.io 주소는 끊김: 유입이 적은 지금 옮기는 게 유리
8. [Claude] Search Console 등록 안내, 사이트맵 `https://topikbank.com/sitemap.xml` 제출. 같은 Cloudflare 계정에서 Web Analytics(무료, 쿠키 없음)도 연결 검토

푸시·저장소 관리는 지금처럼 GitHub Desktop 그대로. 푸시하면 Cloudflare가 자동 빌드.

## 9. 백업과 이전 원칙

- GitHub가 막혀도 로컬 폴더가 원본. 월 1회 외장 하드나 클라우드 드라이브에 복사
- 개인 도메인을 쓰면 Cloudflare Pages, Netlify, VPS(Nginx에 `_site` 업로드)로 1~2시간 안에 이전 가능
- 판매(Gumroad)와 구독자 목록은 GitHub 밖에 둠

## 10. 사용자 작업 스타일

- 한국어로 답변
- 줄표(—) 대신 쌍점(:) 사용
- 불필요한 인사말 생략
- 공개 저장소에 올리는 작업(커밋·푸시, 설정 변경)은 실행 전에 무엇을 올리는지 짧게 알리고 진행

## 11. 참고 자료

- 설계 문서(claude.ai Docs): https://claude.ai/code/artifact/44d781fe-f8c8-48c1-90ca-74966762d582
- 대화 중 만든 Word 문서: `기사활용_수업자료_판매검토.docx`, `AI활용_지문제작_저작권기준.docx`
