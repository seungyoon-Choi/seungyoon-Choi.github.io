# Seungyoon Choi — Personal Homepage

[al-folio](https://github.com/alshedivat/al-folio) 테마 기반. 데모 콘텐츠는 모두 제거하고 CV 내용으로 채워둔 상태입니다.

---

## 1. 배포 (처음 한 번만)

### 1-1. 저장소 만들기

1. GitHub → **New repository**
2. 이름: **`seungyoon-Choi.github.io`**
3. **Public** → Create

### 1-2. 파일 올리기

```bash
cd 이_폴더
git init
git add .
git commit -m "init homepage"
git branch -M main
git remote add origin https://github.com/seungyoon-Choi/seungyoon-Choi.github.io.git
git push -u origin main
```

GitHub Desktop을 쓰신다면 이 폴더를 "Add existing repository"로 등록하고 Publish 하시면 됩니다.

### 1-3. GitHub Pages 설정 (중요)

push하면 **Actions** 탭에서 `Deploy site` 워크플로가 자동으로 돕니다. 빌드는 GitHub이 대신 해주므로 **로컬에 Ruby를 설치할 필요가 없습니다.** 2~4분 걸립니다.

빌드가 끝나면 `gh-pages` 브랜치가 새로 생깁니다. 그 다음에:

**Settings → Pages → Build and deployment**
- Source: `Deploy from a branch`
- Branch: **`gh-pages`** / `(root)` → Save

> 이 설정을 안 하면 Actions는 성공했는데 사이트는 안 뜨거나 마크다운 원본이 보입니다. 가장 흔한 실수입니다.

1~2분 뒤 **https://seungyoon-choi.github.io** 접속.

이후로는 `git push` 할 때마다 자동으로 다시 빌드·배포됩니다.

---

## 2. 지금 채워야 할 것 (placeholder)

| 파일 | 항목 | 할 일 |
|---|---|---|
| `_data/socials.yml` | `scholar_userid` | 비어 있음. Google Scholar 프로필 주소의 `user=` 뒤 문자열 입력 |
| `assets/img/prof_pic.jpg` | 프로필 사진 | 회색 placeholder 이미지임. 본인 사진으로 교체 (같은 파일명) |
| `_news/*.md` | 날짜 | CV에 연도만 있어서 **월/일은 추정치**임. 실제 날짜로 수정 |
| `_bibliography/papers.bib` | 논문 링크 | `pdf`, `code`, `html`, `arxiv` 필드 추가 (아래 참고) |

---

## 3. 내용 수정하는 법

### 소개글 / 연구 관심사
`_pages/about.md` — 위쪽 `---` 사이는 설정, 아래는 본문(마크다운)입니다.

### 논문 추가
`_bibliography/papers.bib` 에 BibTeX 형식으로 추가하면 publications 페이지가 자동 생성됩니다.

```bibtex
@inproceedings{choi2027example,
  abbr        = {NeurIPS},
  title       = {논문 제목},
  author      = {Choi, Seungyoon and Park, Chanyoung},
  booktitle   = {Conference on Neural Information Processing Systems},
  year        = {2027},
  selected    = {true},
  bibtex_show = {true},
  pdf         = {https://arxiv.org/pdf/xxxx.xxxxx},
  code        = {https://github.com/seungyoon-Choi/repo},
  html        = {https://arxiv.org/abs/xxxx.xxxxx},
  abstract    = {초록을 넣으면 펼쳐보기 버튼이 생깁니다.},
  annotation  = {* Equal contribution}
}
```

- `selected = {true}` → 메인 페이지의 selected publications에도 표시
- `abbr` → 왼쪽 학회 배지. 색상은 `_data/venues.yml` 에서 지정
- 연도별 그룹핑·정렬은 자동입니다

### News 추가
`_news/` 안에 `.md` 파일을 하나 만들면 됩니다. 파일명은 자유지만 날짜를 앞에 붙이면 정리가 쉽습니다.

```markdown
---
layout: post
date: 2026-09-01 09:00:00+0900
inline: true
related_posts: false
---

Our paper was accepted to **NeurIPS 2026**. :page_facing_up:
```

`inline: true` = 한 줄 소식. 길게 쓰고 싶으면 `inline: false` + `title:` 추가하면 별도 페이지가 생깁니다.

### CV
`assets/pdf/cv.pdf` 를 새 파일로 덮어쓰면 CV 페이지와 다운로드 버튼이 함께 갱신됩니다.

### 이름·이메일·사이트 설정
`_config.yml` 상단 (`first_name`, `last_name`, `description`, `keywords`, `url` 등).

### Google Analytics
`_config.yml` 의 `analytics: google:` 에 측정 ID(`G-XXXXXXXXXX`)를 넣으면 켜집니다. **지금은 비어 있어 아무 데이터도 수집되지 않습니다.**

---

## 4. 로컬 미리보기 (선택 사항)

안 해도 됩니다 — push하면 GitHub이 빌드해주니까요. 다만 매번 push 없이 확인하고 싶다면 Ruby가 필요합니다.

```bash
gem install bundler
bundle install
bundle exec jekyll serve
# http://localhost:4000
```

macOS에서 `bundle install` 이 실패하면 대개 ImageMagick 때문입니다: `brew install imagemagick` 후 재시도.

---

## 5. 원본 대비 변경 사항

- 데모 콘텐츠 전량 삭제: `_posts`, `_projects`, `_books`, `_teachings`, 데모 이미지/영상/오디오, Einstein 예시 데이터
- 불필요한 페이지 삭제: blog, projects, repositories, teaching, people, books, plugins
- GitHub Actions는 `deploy.yml` 하나만 남김 (나머지는 실패 알림 메일만 유발)
- 외부 RSS 연동(medium.com), Disqus 데모 계정 제거
- 남은 페이지: **about / publications / cv**

---

테마 원본: [alshedivat/al-folio](https://github.com/alshedivat/al-folio) (MIT License, `LICENSE` 파일 참고)
