<h1> Git 특강: 버전관리

> 버전관리가 무엇일까?



<h2>
    개요
</h2>

 일반적인 우리의 버전관리 방식 -> 1, 2, 수정, 최종수정... 등

 자료간의 차이 확인이 어려움 -> 차이가 무엇인지 Log로 기록!



<h3>
    크로미움
</h3>

- 크롬 부라우저의 오픈소스
- 현재까지 1,000,000여개 커밋, 20,000여개의 릴리즈 



<h3>
    버전관리시스템
</h3>

- 대표적으로 **Git** / 다양한 시스템프로그램이 존재





<h2>
    Git
</h2>

 분산버전관리시스템

 리누스 토르발스가 05년에 개발

 변경사한 추적, 여러 사람들과 파일작업 조율



<h3>
    분산버전관리시스템(DVCS)
</h3>

- 중앙에서 버전을 관리. 파일을 받아서 사용

- 원격저장소를 통해 협업. 모든 히스토리(과거버전)를 클라이언트들이 공유

  

<h3>
    기본 흐름
</h3>

작업파일 --> add하여 **Staging area**에 모아 --> **commit**으로 버전 기록

- Git은 파일을 modified , staged, committed로 관리
  - modified :  파일이 수정된 상태
  - staged  : 곧 커밋할 것이라고 표기된 상태
  - committed : 커밋
  
- 기초CLI(Command Line Interface) 명령어 <-> GUI

  - touch xxx.txt  --> txt파일 추가

    ```bash
    $ touch <파일명>
    $ toouch README.md
    ```

  - ls(list), pwd(print working directary)

    ```bash
    $ ls
    1.txt
    $ pwd
    /c/Users/lec.Desktop/실습1
    ```

  - mkdir xxx (make diretory) :  xxx폴더 생성

    ```bash
    $ mkdir test
    ```

  - cd xxx : chane directory 폴더 이동

    ```bash
    $ cd test
    /c/Users/lec.Desktop/실습1/test
    $ cd .. //상위
    $ cd .  //하위 
    ```

  - cd .. : 상위 디렉토리 (cd . :현재 디렉토리)

  - $ git intit : 특정 폴더를 git 저장소를 만들어 git으로 관리

    - git 폴더 생성

      ```bash
      $ git init
      ```

  - $ git add  <file> :  working directory 상의 변경 내용을 staging area에 추가
  
    - untracked, modified 상태의 파일을 staged로 변경
    
  - $ git commit -m '커밋메시지' : 파일들을 커밋을 통해 버전으로 기록
  
    ```bash
    $ git commit -m 'Git.mnd'
    ```
  
  - $ git status, log  : git폴더의 상태 / 로그 기록
  - $ git clone <원격저장소주소>
  
  

<h3>
    파일 라이프사이클

- **Working directory**  - tracked
- **Working directory**  - untracked





<h3>
    분산버전관리시스템(DVCS)
</h3>

> 원격저장소를 활용하여 협업



<h4>
    원격저장소 설정
</h4>

1. [Github]<https://github.com/> 접속 로그인 후, new repositories 생성

2.  원격저장소 주소 가져오기

3.  원하는 폴더에 git 파일 생성 후, 파일 add, commit

4. $ git remote add origin (원격저장소 주소)

5.  commit된 Git폴더를 저장소로 보내기

   ```bash
   $ git push origin master
   ```



<h4>
    원격저장소 설정 명령어
</h4>

- $ git remote -v : remote 확인

- $ git remote add  <이름> <url> :  remote 추가

- $ git remote rm <이름> : remote 삭제

- $ git remote set-url <이름> <url> : remot  url 변경

- $ git remot rename <이름> <새이름> : remot 이름변경

  ```bash
  - $ git remote -v
  - $ git remote add origin github.test
  - $ git remote rm origin
  - $ git remote set-url origin github.TIL
  - $ git remot rename oigin newOrigin
  ```



<h4>
    원격저장소 활용명령어
</h4>

- $ git push <remote이름> <브랜치이름> : 원격저장소로 로컬 저장소 변경 사항(commit)을 올림(push)

- $ git pull  <remote이름> <브랜치이름> : 원격저장소에서 변경된 내역을 받아와 이력을 병합

- $ git clone <remote이름> : 원격저장소를 복제하여 가져오기

  ```bash
  - $ git push origin master
  - $ git pull origin master
  - $ git clone <remote이름>
  ```



---

