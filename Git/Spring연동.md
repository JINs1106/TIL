# Spring - Git 연동

---



## Basic

- WORKSPACE  ---> Github 이용  ---> 로컬 REPOSITORY  ===> COMMIT

  ===> REMOTE REPOSITORY / PUSH

- Git 연동시 id / pw 인증방식 x  ===> 암호화된 **TOKEN** 사용

  - Remotes - origin - change Credentials 에 입력

- Git 연동후 import maven project  : 프로젝트 가져오기

- export로 연동 전 백업 가능  ===> .zip  /  .tar 등



### PULL - PUSH

#### PULL

1. git : local ---> master 혹은 원하는 branch 생성 및 checkout  ===>  master pull & merge
2. JAVA EE : 해당 프로젝트 - TEAM - master pull & merge

### PUSH

- git : 수정 및 업데이트 내용  --->  commit  + message  ===>  push master or branch

