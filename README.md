# y-sihyeon.github.io

개발 블로그 소스입니다. https://y-sihyeon.github.io

Jekyll + [Minimal Mistakes](https://mmistakes.github.io/minimal-mistakes/) 테마(`catppuccin_mocha` 스킨)로 만들고, `master` 에 푸시하면 GitHub Pages 가 1~2분 안에 빌드해 배포합니다.

> 이 README 는 사이트에 올라가지 않습니다(`_config.yml` 의 `exclude`).

---

## 처음 한 번만: 미리보기 환경 준비 (macOS)

macOS 에 기본으로 들어 있는 Ruby 는 너무 오래돼서(2.6) 새로 설치합니다.

```bash
brew install ruby

# Apple Silicon(M1 이후) Mac
echo 'export PATH="/opt/homebrew/opt/ruby/bin:$PATH"' >> ~/.zshrc
# Intel Mac 이면 위 줄 대신
# echo 'export PATH="/usr/local/opt/ruby/bin:$PATH"' >> ~/.zshrc

source ~/.zshrc
ruby -v    # 3.x 가 나와야 합니다. 2.6 이 나오면 PATH 가 안 잡힌 것입니다.
```

그다음 저장소 폴더에서 `bin/serve` 를 실행하면 필요한 것을 알아서 설치합니다(처음 한 번은 몇 분 걸립니다).

`Gemfile` 의 `github-pages` gem 이 GitHub Pages 서버와 **똑같은 Jekyll·플러그인 버전**을 맞춰 주기 때문에, 내 컴퓨터에서 보이는 모습이 실제 사이트와 같습니다.

---

## 글 쓰는 순서

### 1. 새 글 만들기

```bash
bin/new-post <slug> "<제목>" <카테고리>

# 예
bin/new-post cloudflare-tunnel "Cloudflare Tunnel 로 집 서버 열기" Cloudflare
```

`_posts/2026-10-08-cloudflare-tunnel.md` 처럼 오늘 날짜가 붙은 파일이 양식과 함께 만들어집니다.

- **slug**: 글 주소가 됩니다 → `https://y-sihyeon.github.io/posts/cloudflare-tunnel/`. 영어 소문자·숫자·하이픈만. 한 번 올린 뒤에는 바꾸지 마세요(주소가 바뀝니다).
- **제목**: 화면에 보이는 제목. 한글 가능.
- **카테고리**: 아래 표에서 **하나만**.

### 2. 미리보기 하면서 쓰기

```bash
bin/serve
```

브라우저에서 http://localhost:4000 을 엽니다. 파일을 저장하면 자동으로 새로고침됩니다. 끄려면 `Ctrl + C`.

### 3. 올리기

```bash
git add .
git commit -m "글: Cloudflare Tunnel 로 집 서버 열기"
git push
```

1~2분 뒤 사이트에 반영됩니다. 진행 상황은 저장소의 **Actions** 탭에서 볼 수 있습니다.

---

## 카테고리와 태그

| | 카테고리 | 태그 |
| --- | --- | --- |
| 개수 | 글마다 **하나** | 여러 개 자유롭게 |
| 정해진 목록 | `Cloudflare` `네트워크` `CDN` `AI` | 없음 |
| 예 | `categories: Cloudflare` | `tags: [dns, workers, cache]` |

주제가 겹칠 때(예: Cloudflare 의 CDN 캐시 이야기)는 **가장 중심이 되는 것**을 카테고리로, 나머지를 태그로 붙이세요.

```yaml
categories: CDN
tags: [cloudflare, cache, http]
```

카테고리를 새로 만들려면 `bin/new-post` 맨 위의 `CATEGORIES` 에 추가하세요. 철자가 조금만 달라도(`cdn` / `CDN`) 카테고리 페이지에서 따로 묶이기 때문에 목록으로 고정해 두었습니다. (`bin/new-post` 는 대소문자를 알아서 맞춰 줍니다.)

글 주소에는 카테고리가 들어가지 않으므로, 나중에 카테고리를 바꿔도 링크는 깨지지 않습니다.

---

## 자주 쓰는 문법

### 코드 블록

언어 이름을 붙이면 색이 입혀집니다.

````markdown
```bash
curl -I https://example.com
```
````

> **주의**: 웹페이지나 메신저에서 코드를 복사해 붙이면 눈에 안 보이는 문자(폭 없는 공백 등)가 딸려 와서 코드 블록이 깨질 수 있습니다. 미리보기에서 코드 블록이 한 줄로 뭉개져 보이면 ```` ``` ```` 줄을 지우고 직접 다시 쳐 보세요.

### 이미지

이미지는 `assets/images/posts/<slug>/` 에 넣고 이렇게 씁니다.

```markdown
![Cloudflare 대시보드의 DNS 설정 화면](/assets/images/posts/cloudflare-tunnel/dns.png)
```

`[ ]` 안의 설명은 이미지가 안 보일 때와 화면 낭독기에서 쓰이니 비우지 마세요.

### 알림 상자

문단 바로 다음 줄에 붙이면 그 문단이 상자로 바뀝니다.

```markdown
이 설정은 무료 요금제에서도 됩니다.
{: .notice--info}
```

| 클래스 | 용도 |
| --- | --- |
| `.notice` | 기본 |
| `.notice--info` | 참고 |
| `.notice--success` | 팁 |
| `.notice--warning` | 주의 |
| `.notice--danger` | 위험 |
| `.notice--primary` | 강조 |

### 목차

소제목(`##`, `###`)을 쓰면 오른쪽에 목차가 자동으로 생깁니다. 소제목이 없으면 목차 상자는 숨겨집니다. 특정 글에서 끄려면 머리말에 `toc: false`.

---

## 초안

아직 올리고 싶지 않은 글은 둘 중 하나로 두세요.

- 머리말에 `published: false` 를 넣고 커밋 → 사이트에 나오지 않습니다. 다 쓰면 그 줄을 지웁니다.
- `_drafts/` 폴더에 날짜 없이 `cloudflare-tunnel.md` 로 저장 → `bin/serve` 에서만 보이고 배포되지 않습니다. 올릴 때 `_posts/2026-10-08-cloudflare-tunnel.md` 로 옮깁니다.

---

## 파일 구조

| 경로 | 내용 |
| --- | --- |
| `_posts/` | 글 |
| `_pages/` | 소개, 카테고리·태그·글 목록 페이지 |
| `_config.yml` | 사이트 설정(제목, 프로필, 스킨, 분석 도구 등). 바꾼 뒤에는 `bin/serve` 를 다시 켜야 반영됩니다 |
| `_data/navigation.yml` | 상단 메뉴 |
| `assets/css/main.scss` | 한글 글꼴·줄간격 등 스타일 보정 |
| `_includes/head/custom.html` | 웹폰트, 파비콘 |
| `bin/` | 글쓰기 도우미 스크립트 (사이트에는 올라가지 않음) |
