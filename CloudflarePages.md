# Cloudflare Pages 배포 가이드

## 배포 완료 요약

- **프로덕션 URL:** https://krx-sector-map.pages.dev/
- **프로젝트명:** `krx-sector-map`
- **배포 대상 파일 (3개):**
  - `index.html` — 메인 페이지 (KOSPI/KOSDAQ 탭 전환)
  - `KOSPI_treemap.html` — KOSPI 섹터 트리맵
  - `KOSDAQ_treemap.html` — KOSDAQ 섹터 트리맵
- **배포 방식:** Cloudflare Pages (무료 플랜) + Wrangler CLI
- **프로덕션 브랜치:** `master`

---

## 사전 준비

### 1. Wrangler CLI

Cloudflare의 공식 CLI 도구인 `wrangler`를 사용합니다. 별도 설치 없이 `npx`로 실행 가능합니다.

```bash
npx wrangler --version
```

### 2. Cloudflare 로그인

최초 1회 로그인이 필요합니다. 아래 명령어 실행 시 브라우저에서 Cloudflare OAuth 로그인 창이 열립니다.

```bash
npx wrangler login
```

로그인 후 인증 토큰이 로컬에 저장되므로 이후에는 자동 인증됩니다.

### 3. 배포용 디렉토리 (`dist/`)

배포할 파일만 `dist/` 폴더에 모아서 관리합니다. `dist/`는 `.gitignore`에 추가되어 있으므로 git에는 포함되지 않습니다.

---

## 최초 프로젝트 생성 (이미 완료)

프로젝트는 이미 생성되어 있으므로 다시 실행할 필요 없습니다. 참고용으로 기록합니다.

```bash
# 프로젝트 생성 (프로덕션 브랜치를 master로 설정)
npx wrangler pages project create krx-sector-map --production-branch master
```

---

## 배포 방법 (업데이트 시)

treemap HTML 파일이 갱신될 때마다 아래 명령어를 실행합니다.

### Step 1: dist 폴더에 파일 복사

```bash
cp index.html KOSPI_treemap.html KOSDAQ_treemap.html dist/
```

### Step 2: Cloudflare Pages에 배포

```bash
npx wrangler pages deploy dist --project-name krx-sector-map --branch master --commit-dirty=true
```

### 한 줄로 실행

```bash
cp index.html KOSPI_treemap.html KOSDAQ_treemap.html dist/ && npx wrangler pages deploy dist --project-name krx-sector-map --branch master --commit-dirty=true
```

배포 완료 시 아래와 같은 출력이 나타납니다:

```
✨ Success! Uploaded 3 files (2.12 sec)
🌎 Deploying...
✨ Deployment complete! Take a peek over at https://xxxxxxxx.krx-sector-map.pages.dev
```

---

## 주요 명령어 모음

| 용도 | 명령어 |
|------|--------|
| 로그인 | `npx wrangler login` |
| 프로젝트 목록 확인 | `npx wrangler pages project list` |
| 배포 이력 확인 | `npx wrangler pages deployment list --project-name krx-sector-map` |
| 배포 | `npx wrangler pages deploy dist --project-name krx-sector-map --branch master --commit-dirty=true` |
| 프로젝트 삭제 | `npx wrangler pages project delete krx-sector-map` |

---

## 디렉토리 구조

```
krx-sector-map/
├── index.html                 # 메인 페이지 (소스)
├── KOSPI_treemap.html         # KOSPI 트리맵 (소스, 자동 생성)
├── KOSDAQ_treemap.html        # KOSDAQ 트리맵 (소스, 자동 생성)
├── dist/                      # 배포용 폴더 (.gitignore에 포함)
│   ├── index.html
│   ├── KOSPI_treemap.html
│   └── KOSDAQ_treemap.html
├── .gitignore
├── update.sh                  # treemap 자동 갱신 스크립트
└── CloudflarePages.md         # 이 문서
```

---

## 참고 사항

- **무료 플랜 제한:** 월 500회 배포 (`wrangler pages deploy` 1회 = 1회 배포), 무제한 대역폭, 무제한 요청
- **커스텀 도메인:** Cloudflare 대시보드 > Pages > krx-sector-map > Custom domains에서 추가 가능
- **자동 배포:** `update.sh` 스크립트 끝에 배포 명령어를 추가하면 treemap 갱신 시 자동 배포 가능
- **배포 롤백:** Cloudflare 대시보드에서 이전 배포 버전으로 롤백 가능
- **`--commit-dirty=true`:** git에 커밋되지 않은 변경사항이 있어도 경고 없이 배포 진행
