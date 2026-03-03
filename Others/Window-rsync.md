# Window에 rsync 설치





## Rsync란??

- 원격으로 파일과 디렉토리를 동기화하기 위해 사용하는 툴
- 파일이 바뀐 부분만 업로드해서 경로와 동일하게 수정해준다.
- 로컬에서 개발 후 배표를 할 때 rsync를 통해 사용하는데 window 환경에서는 기본적으로 rsync를 지원하지 않아 bash 터미널에서 몇가지 라이브러리를 설치하여 rsunc를 사용 할 수 있음.





### rsync 설치 및 라이브러리 설치

-  https://repo.msys2.org/msys/x86_64/ 를 통해 rsync-버전_x86_64.pkg.tar.zst
- Git에 rsync패키지 복사
  - C:\Program Files\Git\usr\bin\ 경로에 rsync-3.2.3–1-x86_64.pkg\usr\bin\에 있는 rsync.exe파일을 복사
- dependent 패키지를 다운로드 및 같은 경로에 복사
  - 버전은 대충 최신버전 설치해도 문제없는듯?
  - libopenssl 
    - libopenssl-3.3.1-1-x86_64.pkg.tar.zst
  - libxxhash
    - llibxxhash-0.8.2-1-x86_64.pkg.tar.zst
  - libzstd
    - llibzstd-1.5.6-1-x86_64.pkg.tar.zst

