# GIT명령어 모음.

#### **$ git config --global user.name <이름>**

깃 시작 전 이름 셋팅. (전역셋팅 값이며 지역셋팅으로 할때는 --global 없이 입력)



#### **$ git config --global user.email <메일 주소>**

깃 시작 전 메일 주소 셋팅.



#### **$ git config --global -l**

이름,주소 셋팅 값을 볼 수 있다.



#### **$ git config --unset --global user.name(or email)**

이름, 주소 셋팅 값을 지울 수 있다.



#### **$ git config --unset-all --global user.name(or email)**

중복된 값이 있을 때 config 값 모두 삭제



#### **$ git init**

- git 저장소 초기화. git이 폴더를 관리 할 수 있게 하는 명령어, 초기에 한번만 입력.



#### **$ git remote**

- 현재 프로젝트에 등록된 리모트 저장소를 확인할 수 있다.
- $ git remote -v : 현재 등록된 리모트 저장소 확인
- $ git remote add <이름> <git-hub url 주소> git-hub과 연결.
- $ git remote remove <git-hub url 주소> 연결된 주소 끊을수 있음.



#### **$ git clone**

- 원격저장소로 부터 폴더를 모두 복사해오는 명령어
- git init, git remote add 명령어가 자동 실행되서 온다.
- $ git clone <git-hub url>



#### **$ git status**

- 파일들의 가능한 상태를 확인할 수 있다.
- 작업 디렉토리(working directory)와 스테이징 영역(staging area)의 상태를 확인하기 위해 사용한다.



#### **$ git add**

- 작업 디렉토리 상의 변경 내용을 스테이징 영역에 추가하기 위해 사용하는 명령어.



#### **$ git add <파일/디렉토리 경로>**

- 변경 내용의 일부만 스테이징 영역에 넘기고 싶을 때 디렉토리의 경로를 인자로 넘긴다.



#### **$ git add .**

- 현재 디렉토리의 모든 변경 내용을 스테이징 영역으로 넘기고 싶을 때 . 인자로 넘긴다. (상위 디렉토리의 변경 내용은 포함하지 않음)



#### **$ git add -A**

- 작업 디렉토리 상에 어디에 위치하든 항상 동일하게 모든 변경 내용을 스테이징으로 넘긴다.



#### **$ git add -p**

- 각 변경 사항을 터미널에서 직접 눈으로 확인하면서 스테이징 영역으로 넘기거나 또는 제외할 수 있다.



#### **$ git commit -m “commit message**

- 파일 및 폴더의 추가/변경 사항을 저장소에 기록한다.
- 인덱스(staging area)에 등록되어 있는 파일 상태를 기록한다.



#### **$ git push <저장소명> <브랜치명>**

- 로컬 저장소에서 남겨놓은 파일 변경 이력을 원격 저장소로 전송한다.
- -u 옵션을 사용하면 최초 한 번만 저장소명과 브랜치명을 입력하고 이후에 생략 가능하다.



#### **pull vs fetch**

1. $ git pull
   - 원격저장소로 부터 변경된 내용을 가지고 온 후 병합(merge)
   - pull = fetch + merge 와 같은 의미!
2. $ git fetch
   - 원격저장소로 부터 변경된 내용을 가지고 온 후 병합 x
   - 변경된 내역을 가지고 온 후 검토 후에 merge 할 수 있어서 충돌 방지



#### **$ git branch <브랜치명>**

- 브랜치를 생성하는 명령어
- master 브랜치에서 <브랜치명> 이라는 브랜치를 생성한다.



#### **$ git checkout <브랜치명>**

- 현재 master 브랜치에서 <브랜치명> 으로 이동하기 위한 명령어 또는 restore기능 도 있다. 많은 기능이 있어 현재는 switch 명령어와 restore 대체됨.
- b 옵션을 사용하면 브랜치 생성과 체크아웃을 한번에 할 수 있다.



#### **$ git restore <파일명>**

- 워킹 트리의 파일을 복원해 주는 역할.
- $ git restore <파일명> : 특정 파일 HEAD commit으로 복구하기.
- $ git restore --souce <commit hash> <파일 명> : 파일 특정 commit으로 복구하기.
- $ gir restore --staged <파일명> : Staging Area에 올라간 파일 Unstaging시키기.

​	

#### **$ git switch <브랜치명>**

- head를 해당 브랜치로 이동하는 명령어. 워크스페이스를 이동.



#### **$ git merge <브랜치명>**

- 브랜치를 병합하는 명령어
- 협업 과정에서 같은 이름의 파일 안에 수정한 부분이 겹칠 때 충돌(conflit)이 발생 할 수 있다.



#### **$ git rebase**

- 브랜치를 병합하는 명령어로 merge와 같은 기능이지만,
- merge의 경우 병합 할 브랜치에서 기록한 모든 commit이 master의 commit으로 기록된다.
- rebase의 경우 작업 중 남겼던 commmit 중 불필요한 것들을 생략시키고 필요한 commit만 남겨서 master 병합이 가능하다.
- -i는 interactive라는 옵션이다. 해당 옵션을 사용하면 중간에 낀 커밋 메세지를 수정할 수 있다.









[참고]

https://khs613.github.io/github/github-base/

https://bogyum-uncle.tistory.com/125

https://ifuwanna.tistory.com/263

https://blog.outsider.ne.kr/1505
