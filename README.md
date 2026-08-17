# Wiki Starter — Hugo + Decap CMS + GitHub Pages

고객용 지식 베이스 & 자료실 스타터 프로젝트입니다.

## 구조

```
wiki-starter/
├── content/
│   ├── docs/          ← 문서 (마크다운)
│   ├── blog/          ← 공지사항
│   └── downloads/     ← 자료실 (파일 메타)
├── static/
│   ├── files/         ← 업로드된 파일 저장소
│   ├── css/
│   └── admin/         ← Decap CMS (어드민)
├── layouts/           ← Hugo 템플릿
├── .github/workflows/ ← 자동 배포
└── hugo.toml          ← Hugo 설정
```

## 빠른 시작

### 1. GitHub 리포 생성

이 폴더를 새 리포에 푸시합니다:

```bash
cd wiki-starter
git init
git add .
git commit -m "initial commit"
git remote add origin https://github.com/YOUR-USERNAME/wiki-starter.git
git push -u origin main
```

### 2. GitHub Pages 활성화

리포 Settings → Pages → Source를 **GitHub Actions**로 설정합니다.

### 3. Decap CMS OAuth 설정

Decap CMS가 GitHub에 커밋하려면 OAuth가 필요합니다.

**방법 A — Netlify 무료 프록시 (가장 간단)**
1. [Netlify](https://netlify.com)에 가입
2. 이 리포를 Netlify에 연결 (배포는 안 해도 됨, OAuth만 사용)
3. Site settings → Identity → Enable Identity → External Providers → GitHub 추가
4. `static/admin/config.yml`의 `base_url`을 본인 Netlify 사이트 URL로 변경

**방법 B — 자체 OAuth 서버**
- [decap-cms-github-backend](https://github.com/decaporg/decap-cms-github-backend)를 Cloudflare Workers나 Vercel에 배포

### 4. 설정 수정

`static/admin/config.yml`에서:
- `repo`: 본인의 `username/repo-name`으로 변경
- `base_url`: OAuth 프록시 URL로 변경

`hugo.toml`에서:
- `baseURL`: 본인 Pages URL로 변경

### 5. 사용

- **고객 화면**: `https://YOUR-USERNAME.github.io/wiki-starter/`
- **어드민 화면**: `https://YOUR-USERNAME.github.io/wiki-starter/admin/`

어드민에서 글/파일을 추가하면 → GitHub에 커밋 → Actions가 자동 빌드 → 1~2분 후 사이트 반영

## 로컬 개발

```bash
brew install hugo
cd wiki-starter
hugo server -D
# http://localhost:1313 에서 확인
```

## 커스터마이징

- **디자인**: `static/css/style.css` 수정
- **레이아웃**: `layouts/` 내 HTML 수정  
- **새 섹션 추가**: `content/새폴더/` 생성 + `static/admin/config.yml`에 collection 추가
- **커스텀 도메인**: 리포 Settings → Pages → Custom domain 설정 + `static/CNAME` 파일 추가
