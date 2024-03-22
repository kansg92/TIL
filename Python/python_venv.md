# 파이썬 가상환경 생성



1. 가상환경 생성

   `python -m venv <가상환경이름>`

2. 가상환경 활성화

   1. window

      `./<가상환경이름>\Scripts\activate `

   2. unix, linux

      `source ./venv/bin/activate `

3. 생성된 가장환경 목록확인

   `where python`

4. 가상환경 파이썬 설치

   `curl -O https://www.python.org/ftp/python/3.8.12/python-3.9.12.exe`

5. 가상환경 패키지 설치

   ``````cmd
   # 패키지 설치
   pip install <패키지이름>
   # 패키지 목록 확인
   pip list
   # 패키지 업그레이드
   pip install --upgrade <패키지이름>
   # 패키지 삭제
   pip uninstall <패키지이름>
   ``````

   