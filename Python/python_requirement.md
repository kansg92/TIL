# Requirement



파이썬은 가상환경으로 라이브러리를 보통 관리를 한다. 파이썬마다 버전이나 라이브러리 버전이 달라지거나 할 수 있기때문에 관리를하는데, 내가 사용하는 환경이라던지 다른이와 협업을 할때 라이브러리 버전을 맞추기위해  보통 `requirement.txt` 에 라이브러리를 맞추어서 공유하고 저장을하면서 관리를한다. 





### 생성

```python
pip freeze > requirement.txt
```

### pip list

```python
pip list --format=freeze > requirements.txt
```

### 설치

```python
pip install -r requirements.txt
```