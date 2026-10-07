# TOPIK Practice Bank 사이트 시작 안내

GitHub Pages + Jekyll(Minimal Mistakes 테마)로 만든 TOPIK 문제은행 블로그 뼈대입니다.
프로그램 설치 없이 웹 브라우저만으로 올릴 수 있습니다.

## 1. 사이트 올리기 (약 15분)

1. [github.com](https://github.com) 가입 후 2단계 인증 설정
2. 오른쪽 위 **+ → New repository**
   - Repository name: `topik-bank` (원하는 이름 가능, 영어 소문자 권장)
   - **Public** 선택 → Create repository
3. 새 저장소 화면에서 **uploading an existing file** 클릭
4. 압축을 푼 `topik-bank` 폴더 **안의 내용 전체**를 끌어다 놓기 → 아래 **Commit changes**
5. 저장소 **Settings → Pages**
   - Source: **Deploy from a branch**
   - Branch: **main**, 폴더 **/(root)** → Save
6. 1~3분 후 같은 화면 위쪽에 사이트 주소(`https://아이디.github.io/topik-bank/`)가 나타납니다.

## 2. 꼭 바꿀 설정 (`_config.yml`)

GitHub에서 `_config.yml` 파일을 열고 연필 아이콘(Edit)으로 수정합니다. "바꾸세요" 표시된 줄만 고치면 됩니다.

| 항목 | 넣을 값 |
| --- | --- |
| `title` | 사이트 이름 |
| `baseurl` | 기본값 `"/topik-bank"`. 저장소 이름을 다르게 지었다면 `"/저장소이름"`으로 (개인 도메인 연결 후에는 `""`) |
| `repository` | `아이디/topik-bank` |
| `author.name`, `bio` | 본인 정보 |
| Gumroad 주소 3곳 | 본인 Gumroad 스토어 주소 |

> `baseurl`을 맞추지 않으면 디자인이 깨져 보입니다. 가장 흔한 실수입니다.

## 3. 폴더별 역할

| 위치 | 용도 |
| --- | --- |
| `_posts/` | 유형 분석 글. 파일명 `2026-10-10-영문-제목.md` |
| `_shop/` | 상품 소개 페이지. 예시 파일을 복사해서 사용 |
| `_pages/` | 홈, 무료 자료, 상점, 소개, 구독 페이지 |
| `assets/free/` | **무료** PDF만. 유료 파일은 절대 올리지 않기 |
| `assets/images/` | 표지, 샘플 페이지 이미지 (장당 300KB 이하 권장) |
| `_data/navigation.yml` | 상단 메뉴 |

## 4. 새 글 쓰기

1. `_posts` 폴더 → **Add file → Create new file**
2. 파일명: `2026-10-14-topik-i-reading-main-idea.md`
3. 예시 글 맨 위 `---` 사이 머리말을 복사해 제목, 카테고리만 바꾸고 본문 작성
4. Commit → 1~2분 뒤 사이트에 반영

카테고리 이름은 아래 중에서 골라 통일하세요.
`TOPIK I Reading`, `TOPIK I Listening`, `TOPIK II Reading`, `TOPIK II Listening`, `TOPIK II Writing`, `Vocabulary & Grammar`, `Exam Guide`

## 5. 댓글(giscus) 연결 (선택)

1. 저장소 **Settings → General → Features**에서 **Discussions** 체크
2. [giscus.app](https://giscus.app) 접속 → 저장소 이름 입력 → 카테고리 `General` 또는 새 `Comments` 선택
3. 페이지 아래쪽에 표시되는 `data-repo-id`, `data-category-id` 값을 `_config.yml`의 `repo_id`, `category_id`에 붙여넣기

## 6. 개인 도메인 연결 (로드맵 4단계)

1. 도메인 구입 후 DNS에 GitHub Pages 주소 등록 (A 레코드 4개 또는 CNAME)
2. 저장소 **Settings → Pages → Custom domain**에 도메인 입력, **Enforce HTTPS** 체크
3. `_config.yml`의 `url`을 `"https://내도메인.com"`, `baseurl`을 `""`로 변경

## 7. 저작권 체크

- 모든 문제의 지문, 대화, 보기는 직접 작성 (기출문제 복사·변형 금지)
- 신문 기사, 소설, 남의 블로그 글을 지문으로 쓰지 않기
- 이미지와 폰트는 상업적 이용 가능한 것만
