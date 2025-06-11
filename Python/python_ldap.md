# Window환경에서 python ldap설치

widnow환경에서 python-ldap 라이브러리 설치시 오류가 있어서 해결에대한 트러블 슈팅임



설치를 위해서는 미리 빌드된 wheel설치하여 해결하였음.



https://github.com/cgohlke/python-ldap-build/releases

링크에서  python버전에 맞는  wheel파일을 다운로드

가상환경에서 `pip install 'wheel파일경로' `

wheel파일 설치후 ladp라이브러리 인스톨을 하면 정상적으로 작동하였음.