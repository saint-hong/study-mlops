# yaml 형식 정리

## 1. yaml 파일
- 데이터 직렬화에 쓰이는 포멧/양식 중 하나
   - 데이터 직렬화 : 서비스간에 데이터를 전송할 때 쓰이는 포멧으로 전환하는 것
   - 쿠버네티스 마스터에게 요청을 보낼 때 사용
   - XML, JSOn 등 직렬화 포멧 등이 있음
   - .yml, .yaml 등의 포멧 형식
- yaml의 장점
   - 가독성 : 같은 직렬화 포멧인 json 포멧보다 가독성이 좋다.
   - widely-use
      - kubernetes mainfests 명세
      - docker compose 명세
      - ansible playbook 명세
      - github action workflow 명세 
      - 등에 사용할 수 있다.
   - strict-validation : 줄바꿈과 들여쓰기를 사용할 수 있다.

## 2. yaml 문법
- 선언형 인터페이스를 위해서 Desired State를 명시하는 용도로 사용된다.         
- key-value 형태
   - recurcive한 key-value pair의 집합의 형태로 이루어져 있다.
- 주석 처리 : 줄의 맨 앞에 #을 붙여 주석 처리 가능
- 자료형 
   - string : ""로 감싸거나 일반적인 문자열은 그냥 사용해도 됨
      - this is 1st string 또는 "this is 1st string"
      - 반드시 ""를 사용하는 경우
         - 숫자를 문자열로 사용하는 경우 : "123" 
         - 예약어와 겹치는 경우 : "y", "yes", "true" 
         - 특수문자가 포함된 경우 : "a#b", "a : b", "{a + b}" 등
   - integer : 숫자 그대로 사용 : 123, 999
   - float : 소수점 숫자 그대로 사용 : 99.9, 1.24e+03 (1.24 * 10^3)
   - boolean : True, yes, on, False, no, off
   - List : 
      - - 를 사용하여 list를  정의함 
      - ["a", "b"]로도 나타낼 수 있음
      - 어떤 자료형이든 원소로 사용가능
   - multi-line strings
      - | : 빈줄을 \n으로 처리하고 맨 마지막에 \n을 붙인다.
      - > : 빈줄을 제외하고 맨 마지막에만 \n을 붙인다. 
      - |- , >- : 맨 마지막에 \n을 붙이지 않는다.
   - multi-document yaml : --- 구분선을 사용하여 하나의 yaml 파일에 여러개의 yaml document 작성가능

#### yaml 형식 예시
```
# test deployment

apiVersion: apps/v1
kind: Deployment ## 쿠버네티스의 리소스로 디플로이먼트를 정의
metadata: ## 디플로이먼트의 이름과 관리할 어플리케이션을 정의
  name: nginx-deployment
  labels:
    app: nginx
spec:  ## 디플로이먼트의 세부 기능 : replicaSet을 만들고 3개의 pod를 생성하게 끔한다.
  replicas: 3
  selector: ## replicaSet이 관리할 pod를 명시한다.
    matchLabels:
      app: nginx
  template: ## pod에 대한 템플릿 설정
    metadata:
      labels:
        app: nginx
    spec:  ## 도커허브의 nginx:1.14.2 버전의 이미지를 실행하는 nginx 컨테이너를 나타낸다.
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80

```
