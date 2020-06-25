---
title: Github
category: Linux
order: 1
---


# github(version control system) 
  - ref : https://www.youtube.com/watch?v=YQat_D1C-ps
> 용어
  - snapshot : 특정시점 파일의상태(현재상태 모든정보)
  - delta : 파일의 이전 상태와 비교한 변경사항
  - 관리형태
    - 중앙집중식 버전관리시스템(CVCS) : 현시점 데이터 서버연결필요
      - Subversion(SVN) : CVCS 대표 시스템, 파일 모든변경사항 저장
    - 분산 버전 관리 시스템(DVCS) : 로컬,서버간 참조가능
    - 파일을 추적하지않고, 문자와 줄 단위 추적
    - git GUI : sourcetree,gitk
  
> 상태
  - Unmodified : 이전버전과 비교하여 수정된 부분이 없는상태
  - Modified : 이전 버전과 비교하여 수정된 부분이 있는 상태
  - Staged : 저장(커밋)을 위해 준비된 상태(스테이징,staging)
  - Commit : 새로운 버전으로 업로드, 커밋버전별 해쉬(40자리숫자+알파벳조합)
  
> Workflow
  ```
  1) 선언
    $ git init
  2) 필요,불필요 요소정의 (Tracked, Untracked)
  ```

자원사용량 모니터링 : netdata
devops : circleCI
클라우드 컨테이너 개발환경 생성 : groom
github 블로그 수정 : prose.io
루비 : https://www.ruby-lang.org/ko/documentation/installation/
깃헙메뉴얼 : https://git-scm.com/book/ko/v2

참고 :https://theorydb.github.io/envops/2019/05/04/envops-blog-posting-prose-io/



# git stash
- Temporary save modified source code
```
1) modified & tracked files
  - tracked file(already committed)
2) Staged files
  - git added files
  
  $ git stash
  $ git stash save [stash_name]
```
- Usage

```
- check stashed list
  $ git stash list
  
- apply(callback) stash files

  $ git stash apply               // call recent stashed files
  $ git stash apply [stash_name]
  $ git stash apply --index

- delete stash
  $ git stash drop
  $ git stash drop [stash_name]   // delete recent stashed files

- callback&delete shashed files
  $ git stash pop
  
- revert applied stash
  $ git stash show -p | git apply -R
  $ git stash show -p [stash_name] | git apply -R
```

ref : https://moon9342.github.io/jekyll-struct

