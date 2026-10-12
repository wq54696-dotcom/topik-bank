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
| 도메인, Gumroad, giscus, 분석 | 전부 미설정. 예시 주소·이메일은 공개 화면에서 숨김(빈 값이면 버튼·링크 자동 숨김), 댓글은 꺼 둠 |
| SEO 기본 | `url` 설정(사이트맵 절대 주소), 공유 이미지 `og-default.png`, 파비콘, 404·태그 페이지 (2026-10-07) |
| 검수 화면 | https://claude.ai/artifact/PGMUiQvNw9ic5ruTRG97ai (비공개). 저장소 `items`(문항 75개, 출처 문항관리.xlsx 초안) / `reviews`(문항 ID별 `status` pass·fix·todo, `note`). Claude는 `ArtifactData list reviews`로 읽어 원고·PDF·xlsx에 반영 |
| 진행판 | https://claude.ai/artifact/3YrKQL6CM7xwfypweEDte1 (비공개). 저장소 `board/meta`(기준일, 한 줄 요약, 팀 5개, 주차) / `tasks/<ID>`(S 사이트·C 콘텐츠·R 검수·G 판매·M 유입, `status`: done·claude·user·blocked·todo·hold). **작업이 끝나거나 상태가 바뀔 때마다 Claude가 `ArtifactData`로 해당 task와 `meta.updated`를 갱신할 것.** 칸반 5칸(내 차례·Claude 진행·대기·예정·완료). "내 차례"(`status: user`) 카드에는 반드시 바로 일할 수 있는 연결을 넣을 것: `links: [{label, url}]`(첫 링크가 카드 전체 클릭, https만) 또는 `copy: {label, text}`(Claude에게 보낼 답변 양식 복사) |
| 팀 문서 페이지 | https://claude.ai/artifact/STpUBHgmCenyMLpYuLfE8Y (비공개). `팀작업\make_docs_page.py`가 .md 문서를 묶어 생성, 앵커 `#sales #growth #site #review #gumroad`. 문서를 고치면 다시 생성해 같은 경로로 게시. 검수 화면은 `#mini2 #blog #bank30` 앵커로 묶음 바로 열림 |
| 사용자 대기 | 작가 이름(지금은 사이트 이름으로 대체)·소개·연락 이메일, 검수(`Desktop\topik_bank\검수_체크리스트.md`), Gumroad 가입(`유료상품\blank30\gumroad_등록자료.md`), 도메인 구매 |
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
- 한글 폰트: `_includes/head/custom.html`에서 Noto Sans KR(본문)·Noto Serif KR(대제목) 로드
- 디자인: 사용자의 디자인 시스템 "그린 × 웜 크림"(https://claude.ai/artifact/XoGgt9drxZkpvvhGEFBLdw)을 따름. 토큰은 `assets/css/main.scss` 맨 위 `$tb-*` 변수. 크림 바탕, 그린 4단계(제목 #006241 / 강조 #00754A / 다크 #1E3932 / 정답 틴트 #D4E9E2), 금색은 레벨 배지(`.level-badge`, 다크 바탕)에만, 알약형 버튼, 흰 카드(15px, 그림자 한 겹). 그라디언트·밑줄 액센트·사이드 스트라이프 금지. PDF 생성기 3종도 같은 색(인쇄용이라 바탕은 흰색)
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
- `무료자료\`: 무료 미니 테스트 생성기와 PDF (검수 전 원본)
- `베타테스트\`: 베타 테스트 페이지 생성기(`make_beta.py`, `beta_template.html`), 결과 해독기(`decode_result.py`), 받은 결과(`results\`)
- `팀작업\`: 팀별 조사·기획 문서(사이트팀, 판매팀, 유입팀)
- `검수_체크리스트.md`: 사용자용 검수 안내
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

**검수 흐름 (2026-10-12부터 모든 새 콘텐츠에 적용)**

`초안(Claude)` → `베타 테스트(외국인 학습자)` → `사람 검수(사용자)` → `공개·판매`

1. **초안**: 문항을 쓰고 맞춤법 검사 후 문항관리.xlsx에 상태 `초안`으로 등록
2. **베타 테스트 페이지 제작**: `Desktop\topik_bank\베타테스트\make_beta.py`의 `PACKS`에 세트를 추가하고 실행 → 나온 HTML을 Artifact로 게시(이미 올린 묶음은 같은 파일 경로로 다시 게시해 주소 유지). 테스터는 휴대폰·태블릿·PC에서 풀고, 망설인 문항·불명확한 해설·모르는 단어를 표시한 뒤 **결과 코드**(`TOPIKBETA1:...`)를 복사해 사용자에게 보냄. 페이지는 DB를 쓰지 않음(DB를 쓰면 외부 공유 불가)
3. **결과 반영**: 사용자가 코드를 Claude에게 전달 → `python decode_result.py "코드"`로 해독 → 오답·망설임·해설 불명확·메모가 붙은 문항을 정리해 검수 화면의 해당 문항 메모에 "베타: ..."로 기록
4. **사람 검수**: 사용자는 검수 화면에서 베타 표시가 붙은 문항 위주로 확인하고, 나머지는 한국어 자연스러움만 훑음. 최종 수정은 반드시 사용자 판단(저작권상 창작 기여, 미묘한 어감은 원어민만 잡음)
5. **공개·판매**: 통과 문항만 `공개`/`판매`로 변경

- 테스터는 표시와 의견만 남김. 문장을 직접 고쳐 쓰게 하지 않음(권리 관계)
- 유료 상품 묶음(`beta-blank30`)은 믿을 만한 테스터에게만 링크 전달
- 쓰기 51~54처럼 객관식이 아닌 문항은 베타 페이지에서 제외됨(생성기가 보기 4개 문항만 고름). 필요하면 서술형 응답 칸을 추가할 것
- 현재 베타 페이지: 공개 예정 묶음 https://claude.ai/artifact/698rtVFKQHeP7hLHn6dYLH (39문항) / 유료 30제 https://claude.ai/artifact/5jaqq7sF55Fs9bCgZyZZQq (30문항). 둘 다 비공개 상태로 게시했고 공유 범위는 사용자가 Share 메뉴에서 정함

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
   - 무료 미니 테스트 2종 PDF 완성, 검수 대기: `Desktop\topik_bank\무료자료\` (TOPIK I 읽기 10문항 15분, TOPIK II 읽기 10문항 20분). 문항관리.xlsx 47문항(공개 2, 초안 45)
     - 수정은 `make_mini_tests.py`의 TESTS 데이터를 고치고 `python make_mini_tests.py` (Edge 헤드리스 인쇄, Noto Sans KR 내장)
     - 검수 후: PDF를 `assets/free/`로 복사 → `_pages/free.md` 표의 "Coming soon"을 PDF 링크로 교체 → 문항 상태 "공개"
     - PDF 안의 사이트 주소(`SITE` 변수)는 도메인 이전 후 바꿔서 다시 생성
   - 첫 유료 상품 완성, 검수 대기: `Desktop\topik_bank\유료상품\blank30\topik2-reading-blank-30.pdf` (13쪽, 3세트×10문항, 전략·점수표·정답·해설+단서). 문항관리.xlsx 77문항(공개 2, 초안 75)
     - 원고 `questions.py`, 생성 `python build.py` (정답 위치 고정 시드로 균등 배분, 표지·샘플 이미지·answers.csv 함께 생성)
     - 사이트: `assets/images/blank30-cover.jpg`, `blank30-sample-1.jpg`(1~3번만), `_shop/topik2-reading-blank-30.md` 갱신
     - 상품 페이지: `gumroad_url`이 비어 있으면 "Coming soon · Get notified"(구독 페이지) 버튼, 채우면 구매 버튼으로 자동 전환
   - 다음: 사용자 검수 → Gumroad 등록(로드맵 3번). 가격 $5 제안 그대로인지 확인 필요
   - 쓰기 모범 답안 글자 수: 53번 238자, 54번 약 660자 (공백 포함, 문단 들여쓰기 1칸씩 포함)
   - 다음 유료 상품 후보: TOPIK II 쓰기 51~54 자료 ($7~12). 쓰기 초안 글의 상품 박스는 현재 `/subscribe/`로 연결("coming soon")
3. 판매 연결: Gumroad 가입·은행 연결, 상품 등록, 구독자 할인 코드, 상품 페이지 링크 교체, giscus·분석 연결
4. 공개·유입: 개인 도메인 연결 + Cloudflare Pages 이전(아래), Search Console 사이트맵 제출, Reddit·Pinterest 등에 무료 자료 공유, 주 1~2편 발행

### 참고 사이트 분석에서 나온 개선안 (2026-10-12, ac-fle.ru: 프랑스어 FLE 학습 자료 사이트)

구조와 메뉴 구성만 참고. 진행판 카드 C11~C13, S9, M6.

| 순위 | 개선안 | 조건 |
| --- | --- | --- |
| 1 | **TOPIK I / TOPIK II 허브 페이지**: 영역·문항 번호 표에서 각 유형 글로 연결(없는 글은 링크 없이 "coming soon" 대신 그냥 텍스트) | 바로 가능 |
| 2 | **사이트에서 바로 푸는 온라인 미니 테스트**: `베타테스트\beta_template.html`의 풀이·채점 기능을 사이트용으로 옮김 | 무료 문항 검수 후 |
| 3 | **글 상단 레벨 배지**(`.level-badge`, 예: TOPIK I · Level 1-2) | 글 발행 시작할 때 |
| 4 | **Toolbox 메뉴**: 접속 표현 정리표, 신문 기사 제목 어휘, 원고지 쓰는 법 | 공개 글 10편 이상 |
| 5 | 다국어 안내 페이지(베트남어·중국어 등) | 영어 글이 자리 잡은 뒤 판단 |

따라 하지 않을 것: 기출문제 배포("공식 기출 무료 제공"), 시판 교재 목록·파일 제공, 외부 광고 링크, "곧 제공" 빈 메뉴와 예시 연락처를 공개 화면에 두는 것.

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

**사전 점검 결과 (2026-10-12, `Desktop\topik_bank\팀작업\사이트팀\cloudflare_이전_준비.md`)**: 실제 빌드는 못 돌려 봄. 이전할 때 함께 적용할 것:
- Ruby 3.3.4 고정(`.ruby-version` 또는 `RUBY_VERSION`): Cloudflare 기본 Ruby가 더 높아 `github-pages` gem 빌드가 실패할 수 있음
- 3단계의 `--baseurl ""`만으로는 `url`이 github.io로 남아 canonical·사이트맵 주소가 틀림 → `_config.cloudflare.yml`(url, baseurl 덮어쓰기) + `--config _config.yml,_config.cloudflare.yml` 방식으로
- 환경 변수 `JEKYLL_ENV=production` 추가, `Gemfile`에 `github-pages` 버전 명시(권장)
- 도메인 연결 후 사이트 주소가 박힌 곳도 교체: PDF 생성기 2개의 `SITE` 변수(PDF 재생성), `gumroad_등록자료.md`
- **순서 권고**: 무료 PDF 공개, Gumroad 등록, 외부 홍보는 도메인 이전 뒤에 하는 것이 안전(주소가 PDF와 홍보 글에 들어감)

다른 팀 문서: `팀작업\판매팀\쓰기상품_기획안.md`(쓰기 51~54 상품 36문항·$9 제안), `팀작업\유입팀\발행일정_홍보문안.md`(9편 발행 일정 10/20~11/17, Reddit·Pinterest 문안, Search Console 절차)

## 9. 백업과 이전 원칙

- GitHub가 막혀도 로컬 폴더가 원본. 월 1회 외장 하드나 클라우드 드라이브에 복사
- 개인 도메인을 쓰면 Cloudflare Pages, Netlify, VPS(Nginx에 `_site` 업로드)로 1~2시간 안에 이전 가능
- 판매(Gumroad)와 구독자 목록은 GitHub 밖에 둠

## 10. 사용자 작업 스타일

- 한국어로 답변
- 줄표(—) 대신 쌍점(:) 사용
- 불필요한 인사말 생략
- 진행 상황·팀 작업 결과 보고는 칸반 형식으로: `내 차례 / Claude 진행 / 대기 / 예정 / 완료`, 카드마다 팀 이름. 서술형으로 길게 쓰지 않음
- 공개 저장소에 올리는 작업(커밋·푸시, 설정 변경)은 실행 전에 무엇을 올리는지 짧게 알리고 진행

## 11. 참고 자료

- 설계 문서(claude.ai Docs): https://claude.ai/code/artifact/44d781fe-f8c8-48c1-90ca-74966762d582
- 대화 중 만든 Word 문서: `기사활용_수업자료_판매검토.docx`, `AI활용_지문제작_저작권기준.docx`
