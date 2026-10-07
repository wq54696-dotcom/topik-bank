# CLAUDE.md: TOPIK Practice Bank 인수인계서

작성일: 2026-10-07 (claude.ai 대화에서 Claude Code로 인계)

## 1. 프로젝트 한 줄 요약

외국인 TOPIK 수험생을 대상으로, 무료 유형 분석 글과 미니 테스트로 유입을 만들고 **직접 창작한** 유료 문제은행·모의고사 PDF를 Gumroad로 판매하는 영어 중심 정적 블로그.

## 2. 현재 상태

| 항목 | 상태 |
| --- | --- |
| GitHub 계정 | `wq54696-dotcom` (가입·로그인 완료) |
| 저장소 | `wq54696-dotcom/topik-bank`, Public, **빈 저장소로 생성만 됨** |
| 사이트 파일 | 이 폴더에 준비 완료, **아직 커밋·푸시 전** |
| GitHub Pages | **아직 켜지 않음** |
| 로컬 빌드 검증 | 안 됨 (이전 환경에서 rubygems 접근 불가). YAML 문법과 Liquid 괄호 짝만 점검함 |
| 도메인, Gumroad, giscus, 분석 | 전부 미설정 (설정값은 빈칸 또는 예시값) |
| 사용 도구 | Windows PC, GitHub Desktop 사용 중 |

## 3. 바로 할 일 (순서대로)

1. 이 폴더 내용을 저장소에 커밋하고 푸시
   - 커밋 메시지 예: `Initial site skeleton (Jekyll + Minimal Mistakes)`
2. GitHub 저장소 Settings → Pages: Source `Deploy from a branch`, Branch `main`, `/ (root)`
3. Actions 탭에서 빌드 성공 확인, `https://wq54696-dotcom.github.io/topik-bank/` 접속 확인
4. 빌드 실패 시 로그의 파일·줄 번호 기준으로 수정 (가장 흔한 원인: 머리말 YAML, `remote_theme` 버전, Liquid 문법)
5. `_config.yml`의 "바꾸세요" 항목을 사용자에게 물어 채우기: `title`, `author.name`, `author.bio`, Gumroad 주소 3곳, `repository`는 `wq54696-dotcom/topik-bank`로 이미 알 수 있으니 바로 수정
6. 로컬 미리보기 환경 구성 (선택): Ruby + `bundle install` + `bundle exec jekyll serve`. Windows라면 RubyInstaller(Devkit 포함) 필요

## 4. 기술 구성

- 정적 사이트: Jekyll, GitHub Pages 기본 빌드 (`github-pages` gem 기준)
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
3. 판매 연결: Gumroad 가입·은행 연결, 상품 등록, 구독자 할인 코드, 상품 페이지 링크 교체, giscus·분석 연결
4. 공개·유입: 개인 도메인 연결(HTTPS), Search Console 사이트맵 제출, Reddit·Pinterest 등에 무료 자료 공유, 주 1~2편 발행

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
