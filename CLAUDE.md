# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 이 저장소의 정체

- 고도몰 개발자 센터(`고도몰 개발자 센터`, Docusaurus v3.9.2, ko 로케일)의 **빌드 결과물만** 담긴 `gh-pages` 브랜치다. 원격은 `yunsang-j/gd-dev-prototype` 이고, 공개 주소는 `https://yunsang-j.github.io/gd-dev-prototype/` 이다.
- `package.json`, `docusaurus.config.*`, 마크다운 원고, 스크립트가 여기에는 없다. 따라서 이 폴더에서 실행할 빌드·린트·테스트 명령은 없다.
- 브랜치 역사는 스쿼시된 커밋 하나뿐이다. 배포 때마다 통째로 덮어써지므로, 여기서 직접 고친 파일은 다음 배포에서 사라진다고 가정한다.
- 이름 그대로 프로토타입(미리보기) 사이트다. 모든 페이지에 `robots: noindex, nofollow` 가 박혀 있고, 커밋 메시지는 `preview: ...` 접두어를 쓴다.
- 원본 소스 저장소는 `godomall-developers.github.io` 로 추정되지만 이 컴퓨터에서는 찾지 못했다(`../workspaces/godomall-developers.github.io` 는 빈 폴더). 원고·설정 변경 요청이 오면 원본 저장소 위치부터 사용자에게 확인한다.

## 여기서 직접 손대도 되는 것 / 안 되는 것

- 직접 수정 가능: 리다이렉트 스텁(`release-notes-godo25/`, `release-notes-godo26/`, `source-diff-godo25/**`, `source-diff-godo26/**`), 단독 페이지 `template-review/index.html`, `.nojekyll`. 이들은 Docusaurus 가 만들지 않은 파일이다.
- 수정 금지: `assets/` 의 해시 붙은 번들, `search-index.json`, `guide/**`·`release-notes-*.html`·`source-diff-*` 같은 Docusaurus 산출 HTML. 내용을 바꾸려면 원본 저장소에서 다시 빌드해야 한다.
- 모든 내부 링크는 `baseUrl = /gd-dev-prototype/` 를 전제로 한다. 새 스텁이나 단독 페이지를 만들 때도 절대 경로에 이 접두어를 붙인다.

## 사이트 구조와 이름 규칙

- `guide/**`: 개발가이드 문서. 사이드바 분류는 이해하기 / 준비하기 / 커스터마이징 하기 / 커스터마이징 예시 / 잘못된 예시 / 업그레이드 가이드 / 운영자 가이드.
- 런타임 코드 세 자리 숫자가 릴리즈노트와 소스 diff 페이지를 묶는다.

| 코드 | 의미 |
|---|---|
| 725 | PHP 7 · GODO25 |
| 825 | PHP 8 · GODO25 |
| 826 | PHP 8 · GODO26 |

- `release-notes-<코드>.html`: 해당 런타임의 릴리즈노트 한 장. 상단 탭으로 전체 보기 / 스킨 패치 등을 필터링하고, 각 항목이 아래 소스 diff 페이지로 링크된다.
- `source-diff-<코드>.html`: 소스 diff 목록. 상세 페이지는 두 종류다.
  - `source-diff-<코드>/<이슈번호>.html`: 이슈 단위 소스 변경 비교(highlight.js 사용).
  - `source-diff-<코드>/<YYYY-MM-DD>.html`: 스킨 패치 날짜 단위 "소스 변경 전체 보기".
- 구 주소 호환: `*-godo25` → `*-825`, `*-godo26` → `*-826` 으로 보내는 meta refresh + JS 스텁이다. 이슈번호 하위 폴더까지 1:1 로 대응한다. 새 이슈 페이지가 825/826 에 추가되면 대응 스텁도 함께 만들어야 구 링크가 살아 있다.
- `template-review/index.html`: 가이드 문서 가독성 AS-IS / TO-BE 비교용 단독 HTML. Docusaurus 와 무관하며 NCDS 어드민 CSS(`@ncds/ui-admin/1.8`, CDN)를 쓴다. Docusaurus 페이지들도 같은 CDN CSS 를 `<head>` 에서 불러온다.
- 검색은 `@easyops-cn/docusaurus-search-local`(lunr) 이고 색인이 `search-index.json` 이다. 문서를 바꾸면 이 파일도 재빌드로 갱신되어야 한다.

## 로컬 미리보기

Docusaurus 링크가 확장자 없는 경로(`/guide/intro`)를 쓰므로, 클린 URL 을 지원하지 않는 정적 서버에서는 404 가 난다. GitHub Pages 는 이를 알아서 처리한다. 확장자 없는 경로를 `.html` 로 되돌려 주는 서버(예: `npx serve`)로 **상위 폴더**를 서빙하고 `http://localhost:<포트>/gd-dev-prototype/` 로 접근해야 `baseUrl` 이 맞는다.

## 배포

`gh-pages` 브랜치에 푸시하면 그대로 공개된다. 원본 저장소의 배포가 브랜치 전체를 덮어쓰므로, 여기서 수동으로 커밋할 일이 있으면 그 사실을 사용자에게 알리고 원본 쪽에도 반영할 방법을 함께 정한다.
