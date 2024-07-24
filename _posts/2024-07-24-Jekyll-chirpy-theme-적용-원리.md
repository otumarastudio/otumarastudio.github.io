---
title: GitHub Pages와 Jekyll로 만드는 Github 블로그의 원리의 이해
date: 2024-07-24 12:00:00 +0900
categories: [Blogging, Tutorial]
tags: [github-pages, jekyll, ruby, chirpy-theme, 정적사이트, 웹개발, 무료블로그만들기]
---

# 개요

최근 마크다운 기반의 블로그 작성에 대한 욕구가 생겨 알아보던 중 GitHub Pages를 활용한 블로그(일명 github.io 블로그)를 알게 되었습니다. 
여러 테마들을 살펴본 결과, Chirpy 테마가 가장 깔끔하고 안정성이 높아 보여 이를 선택하게 되었고, 여러 가이드라인을 따라 초기 설정을 진행하였죠. 
한 단계씩 이렇게 하면 된다 라는 가이드라인은 많았으나, 이 과정에 대해 체계적으로 정리하고 그 근본적인 원리를 이해하고자 하는 글은 별로 없는 것 같아 이 글을 통해 정리 해보고자 합니다.

GitHub Pages와 Jekyll을 사용한 블로그 구축은 여러 기술과 도구가 조화롭게 작동하는 복잡한 프로세스입니다. 이 문서에서는 이 과정의 핵심 구성 요소, 작동 원리, 그리고 각 단계에 대해 상세히 설명합니다. 이를 통해 단순히 가이드라인을 따르는 것을 넘어서, 전체 시스템의 작동 방식을 이해하고 더 효과적으로 블로그를 운영할 수 있는 인사이트를 제공하고자 합니다.


## 주요 구성 요소들의 용어 정리(아래에 더 자세히)

1. **Ruby**: 프로그래밍 언어
2. **Ruby Gems**: Ruby 프로그램과 라이브러리의 패키지 시스템
3. **Jekyll**: 정적 사이트 생성기
4. **Chirpy Theme**: Jekyll용 인기 있는 블로그 테마
6. **Bundler**: Ruby gem 의존성 관리 도구
7. **Git**: 버전 관리 시스템
8. **GitHub**: 코드 호스팅 및 협업 플랫폼
9. **GitHub Pages**: 정적 웹사이트 호스팅 서비스
10. **GitHub Actions**: 자동화된 워크플로우 실행 도구


# Github.io 블로그 초기 설치와 운영 프로세스

## Github.io 블로그 초기 설치 프로세스

1. **환경 설정**
   - Ruby 설치
   - Bundler 설치: `gem install bundler`

2. **GitHub 저장소 설정**
   - GitHub에서 새 저장소 생성 (예: username.github.io)
   - Chirpy 테마의 starter template 사용 또는 직접 fork

3. **로컬 환경 설정**
   - 저장소 클론: `git clone https://github.com/username/username.github.io.git`
   - 프로젝트 디렉토리로 이동
   - 의존성 설치: `bundle install`

4. **설정 파일 수정**
   - `_config.yml` 파일 수정 (사이트 제목, 설명, URL 등)
   - 불필요한 파일 제거 (예: `_posts` 폴더의 샘플 포스트)

5. **GitHub Pages 및 Actions 설정**
   - `.github/workflows/pages-deploy.yml` 파일 확인 및 필요시 수정
   - GitHub 저장소 설정에서 Pages 소스를 'GitHub Actions'로 설정

6. **초기 커밋 및 푸시**
   - `git add .`
   - `git commit -m "Initial commit"`
   - `git push origin main`

7. **배포 확인**
   - GitHub Actions에서 워크플로우 실행 확인
   - `https://username.github.io`에서 사이트 접속 확인


## Github.io 블로그 운영 프로세스

1. **새 포스트 작성**
   - `_posts` 폴더에 새 마크다운 파일 생성 (형식: `YYYY-MM-DD-title.md`)
   - 파일 상단에 YAML front matter 작성 (제목, 날짜, 카테고리, 태그 등)
   - 마크다운으로 포스트 내용 작성

2. **로컬에서 미리보기**
   - `bundle exec jekyll serve` 실행
   - `http://localhost:4000`에서 변경사항 확인

3. **변경사항 커밋 및 푸시**
   - `git add .`
   - `git commit -m "Add new post: title"`
   - `git push origin main`

4. **배포 및 확인**
   - GitHub Actions에서 자동 빌드 및 배포 과정 모니터링
   - 실제 사이트에서 새 포스트 확인

5. **지속적인 관리**
   - 정기적으로 `bundle update`로 의존성 업데이트
   - Chirpy 테마 업데이트 확인 및 적용
   - 댓글 관리, 분석 도구 모니터링 등


# 이 과정에서 사용 된 여러 용어들의 개념에 대해

### Ruby
- 동적 객체 지향 프로그래밍 언어
- 간결함과 생산성을 강조한 동적인 오픈소스 프로그래밍 언어
- `gem` 명령어를 통해 패키지(gem) 관리
- github가 Ruby로 개발되었음. 그래서 github pages를 통한 홈페이지 제작 지원 프로그램에 jekyll 프레임워크를 기본적으로 지원함.

### Jekyll (https://jekyllrb.com/)
- Ruby 기반의 정적 사이트 생성기(프레임워크)
- 마크다운, Liquid 템플릿, HTML, CSS를 정적 웹사이트로 변환
- 블로그 친화적 기능 제공 (포스트, 페이지, 레이아웃 등)

### Bundler
- Ruby 프로젝트의 gem 의존성 관리 도구
- `Gemfile`을 사용하여 필요한 gem 버전 명시 및 설치
- `bundle exec` 명령어로 일관된 환경에서 Ruby 스크립트 실행

### Chirpy Theme
- Jekyll을 위한 기능이 풍부한 반응형 블로그 테마
- 깔끔한 디자인과 다양한 기능 제공 (카테고리, 태그, 검색, SEO 최적화 등)
- GitHub Pages와의 호환성이 뛰어나며, 쉬운 커스터마이징 가능
- 활발한 커뮤니티 지원으로 지속적인 업데이트와 문제 해결 용이

### Git
- 분산 버전 관리 시스템
- 코드 변경사항 추적 및 협업 지원
- 주요 명령어: `init`, `add`, `commit`, `push`, `pull`

### GitHub
- Git 저장소 호스팅 플랫폼
- 협업, 코드 리뷰, 이슈 트래킹 기능 제공
- GitHub Pages와 GitHub Actions 서비스 제공

### GitHub Pages
- 정적 웹사이트 무료 호스팅 서비스
- GitHub 저장소에서 직접 웹사이트 게시 가능
- 사용자명.github.io 형식의 URL 제공

### GitHub Actions
- CI/CD(지속적 통합/지속적 배포) 도구
- YAML 파일로 워크플로우 정의
- 코드 푸시, PR 등의 이벤트에 반응하여 자동 실행


# 결론

GitHub Pages와 Jekyll을 이용한 블로그 구축은 여러 기술과 도구의 조합으로 이루어집니다. Ruby와 Jekyll이 로컬 개발 환경을 제공하고, Git과 GitHub가 버전 관리와 협업을 지원하며, GitHub Actions가 자동화된 빌드 및 배포를 담당합니다. 이 모든 요소가 조화롭게 작동하여 효율적이고 유지보수가 쉬운 블로깅 플랫폼을 만들어 내는 것이죠.

이 시스템의 이해는 단순히 블로그 운영을 넘어서, 현대적인 웹 개발 및 배포 프로세스에 대한 통찰을 제공합니다. 지속적인 학습과 실습을 통해 이 플랫폼의 잠재력을 최대한 활용할 수 있게 되길 바라며 글을 마치겠습니다.

