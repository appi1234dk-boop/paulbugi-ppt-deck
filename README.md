# Paul's Decks — Vercel 배포

발표자료 포트폴리오 사이트. 메인 페이지에서 각 PPT로 이동할 수 있다.

## 폴더 구조

```
vercel/
├── index.html                  # 메인 페이지 (PPT 카드 목록)
├── vercel.json                 # cleanUrls 설정
├── levelup_diary_intro/
│   └── index.html              # /levelup_diary_intro 로 접속
└── ddalkak_youtuber/
    └── index.html              # /ddalkak_youtuber 로 접속
```

## 로컬 미리보기

```bash
cd vercel
python3 -m http.server 8000
# http://localhost:8000 접속
```

또는 Vercel CLI로:
```bash
npx vercel dev
```

## Vercel 배포

### 처음 배포할 때

1. Vercel CLI 설치 (없으면):
   ```bash
   npm i -g vercel
   ```
2. 이 폴더에서 배포:
   ```bash
   cd /Users/paul/Desktop/bookduck/ppt_make_team/vercel
   vercel
   ```
3. 처음에는 프로젝트명/스코프 등을 묻는다. 답하고 나면 프리뷰 URL이 발급됨.
4. 운영 도메인으로 올리려면:
   ```bash
   vercel --prod
   ```

### Git 연동 배포 (권장)

이 폴더를 GitHub 레포로 올린 뒤 Vercel 대시보드에서 Import → Root Directory를 `vercel` 로 지정하면 자동 배포된다.

## 새 PPT 추가하는 법

1. 새 슬러그 폴더 만들기:
   ```bash
   mkdir vercel/<slug>
   ```
2. 슬라이드 HTML을 `index.html` 이름으로 복사:
   ```bash
   cp outputs/<날짜>_<주제>.html vercel/<slug>/index.html
   ```
3. **슬라이드가 로컬 이미지를 참조하면** (`<img src="assets/...">` 등), 같은 상대경로로 자산도 함께 복사:
   ```bash
   cp -R outputs/assets vercel/<slug>/assets
   ```
   확인: `grep -o 'src="[^"]*"' vercel/<slug>/index.html | grep -v -E 'data:|https?://'`
4. `vercel/index.html` 의 `.grid` 안에 카드 `<a class="card" href="/<slug>">` 한 개 추가
5. `vercel --prod` 로 재배포

## URL

- `메인.com/` → 메인 페이지
- `메인.com/levelup_diary_intro` → 레벨업 다이어리 발표
- `메인.com/ddalkak_youtuber` → 딸깍 유튜버 발표
