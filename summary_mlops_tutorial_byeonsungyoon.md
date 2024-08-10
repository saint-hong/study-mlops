# MLops summary
- 머신러닝을 연구하고 상용화하는 과정을 안정적이고 효율적으로 관리하기 위한 프로세스
   - 변성윤님의 깃헙을 기준으로 정리함 

## 머신러닝 프로세스 - research단계와 product 단계 
- **research** :
   - 연구와 테스트 단계
   - 문제정의 - EDA - feature 생성 - 모델 학습 - 예측
   - 내 컴퓨터 또는 서버에서 실행하는 단계
   - 고정된 데이터를 사용함
- **product** :
   - 상용화 단계 : 머신러닝 모델을 실제 서비스화하는 과정
   - reserch 단계에서 만든 모델을 실제 서비스 환경에서 실행하면 많은 변수와 버그들이 발생함
   - input 데이터가 모델 구현 단계의 데이터와 동일한 범위인지, 다른지 등의 확인 필요
   - 새로 배포한 모델의 성능을 지속적으로 모니터링 해야함
   - research 단계에서 성능이 좋았던 모델이 product 단계에서 사용 못할 수도 있음
- **머신러닝 프로세스의 여러 분야**
   - configuration : 구성
   - data collection : 수집
   - feature extraction : 특징 추출
   - monitoring : 모니터링
   - data varification : 데이터 검증
   - machine resource management : 기계의 자원 관리
   - anlaysis tools : 분석 도구
   - process management tools : 과정 관리 툴
   - serving infrastructure : 서비스 인프라
   - monitoring : 모니터링 
   - ML coding : 머신러닝 코딩 (매우 작은 분야)
- 머신러닝 프로세스가 머신러닝 모델 개발과 머신러닝 모델 운영으로 나뉘게 된다.

## ML + Ops = MLOps
- `머신러닝 모델 개발과 운영 workflow의 간극을 줄이기 위해 생긴 분야`
- 머신러닝 엔지니어링 + 데이터 엔지니어링 + 인프라
   - 머신러닝 모델 개발(ML)과 머신러닝 모델 운영(Ops)에서 발생하는 문제들의 반복을 최소화하고 비즈니스 가치를 창출하는 것이 목표
   - 모델링에 집중할 수 있도록 관련된 인프라를 만들고, 자동으로 운영되도록 하는 과정
   - MLOps는 빠른 시간내에 가장 적은 위험 부담으로 아이디어 단계부터 프로덕션까지 ML프로젝트를 진행할 수 있도록 기술적 마찰을 줄이는 과정
- **model development / model prediction** 으로 세분화 됨
- **ml model development** :
   - training data ingestion : 트레이닝 데이터 수집(섭취)
   - data cleaning : 데이터 전처리
   - feature engineering : 여러 모델들을 만들고 특징 벡터들의 성능을 테스트함, 실험함, 
   - model selection / parameter search : 성능이 좋은 모델을 선택, 모델의 여러가지 파라메터들을 연구
   - persisted model : 지속할 수 있는 모델
- **ml prediction with trained model** : 훈련된 모델에 의한 예측 과정 (development의 persisted model의 성능 연구)
   - unseen data ingestion : 보이지 않는 데이터 수집(트레이닝 데이터에 포함되지 않았던 데이터)
   - data cleaning : 데이터 전처리
   - data transformation info features : 데이터 변환 정보 기능
   - model prediction : 모델 예측
   - result : 결론
- **즉 MLOps 는 머신러닝 모델을 서비스화하기 위한 세분 단위들의 연관성을 효율적으로 조정한 업무 프로세스의 의미**
- 머신러닝이 고도화 되고 서비스가 다변화 되면서 생기는 업무적 문제 상황들
- 실무적 차원에서 머신러닝 팀이 작은 경우
   - 소수의 모델 운영
   - 각자의 모델을 자신만의 방법으로 진행 상황추적, 성능 확인 가능
- 팀이 성자하면서 생기는 새로운 상황들
   - 데이터의 복잡도가 증가하기 시작함
   - 데이터 전처리 work flow가 길어짐
   - 데이터 전처리가 중앙에서 표준화 되지 않고 여기저기에서 갑자기 수정되는 일들 발생
   - 이러한 flow 를 관리하는게 어려워짐
- 사람마다 선호하는 프레임 워크가 다름
   - tensorflow, R, spark, keras, pytorch, MXnet 등... !!!! 나도 주특기인 프레임 워크를 가져야 할 거 같다.
- 모델을 배포하는 serving이 어려워진다.
   - 환경마다 실행이 달라지고, 라이브러리, 파이썬등의 버전에 민감해짐.
   - 모델을 배포한 후 성능이 좋지않을때 다시 과거 버전으로 롤백하는 과정도 복잡해질 수 있다.
- **이러한 복잡도들이 높아지면 결국 어디에서 오류, 버그 가 일어나는지 파악이 어려워지게 된다.**
   - 데이터 사이언티스트 들은 파이프라인의 문제라고 할 수 있고
   - 데이터 엔지니어들은 모델의 문제라고 할 수 있다. 

## MLOps의 목표
- `머신러닝 모델개발(ml dev)과 머신러닝 모델운영(Ops)에서 발생하는 문제들을 최소화하고, 비즈니스의 가치를 창출하기 위함`
   - 모델링에 집중할 수 있도록 안정된 인프라 구축, 운영을 자동화 함
   - research에서 production까지 최소시간으로 risk를 관리하면서 기술적 마찰을 줄이기 위함

## MLOps의 중요 원칙
- reproducibility : 재현성
   - research 단계에서 만든 모델이 production 환경에서도 재현되어야 한다. reproducibility
   - training data, tset data, real data가 유사한 분포를 가져야한다.
- orchestration : 오케스트레이션, 편성
   - 서비스의 자동화된 설정, 관리, 조정 등이 이루어져야 한다.
   - 예측에 대한 수요가 높아지면 내부 서버 증설 필요


## 데이터 직군들의 task : MLOps 관점에서
- data scientist : 모델 개발 ml dev
- data engineer : 파이프 라인 개발
- ml ops engineer : 모델, 파이프라인 및 production 부분 담당

## research ml과 production ml의 차이 
- research ml / production ml : 
   - 데이터 : 고정됨 / 계속해서 변한다 
   - 중요요소 : 모델의 성능 (accuracy, rmse) / 모델성능, 빠른 inference 속도, 해석 가능해야함
   - 도전과제 : 더 좋은 성능을 내는 모델, 새로운 구조의 모델개발 / 안정적인 운영, 전체 시스템 구조
   - 학습 : 모델구조, 파라미터 기반의 재학습 / 데이터가 변경됨로 모델을 재학습시킴
   - 목적 : 논문 출판 / 서비스에서 문제 해결
   - 표현 : offline / online

## MLOps component
- 요리하는 과정에 비유
   - **research** : 집에서 혼자 요리개발하는 과정
      - 집에서 맛있게 먹은 요리가 꼭 레스토랑에서 잘 팔리는 것은 아니다. 
      - 메뉴에 오르지 못할 수 도 있다.
   - **production** : 레스토랑에서 요리를 판매하는 환경
      - 재료 : data, feature
      - 음식 : 머신러닝모델
      - 요리하는 행위 : train
- **프로세스 세분화 비교**
   - Serving
   - Experiment, Model Management
   - Feature store
   - data validation
   - continuous training
   - monitoring
   - gpu infra management
   - auto ml

## Serving 
- 레스토랑에서 만든 음식을 손님에게 서빙하는 단계
- 머신러닝 모델도 소비자에게 서빙하는 것과 같다고 생각할 수 있다.
- Serving 에서 중요한 부분
   - 의존성 관리 : 라이브러리, 파이썬 버전, os 등
   - docker나 kubernetes를 많이 사용함
- **Serving 방식**
   - batch serving
   - online serving
   - edge serving (mobile)
- **Batch Serving**
   - 특정 시간에 서빙하는 개념, 가장 쉬운 방식
   - batch로 많은 양을 한꺼번에 처리하는 의미
   - 방식 : airflow나 cronjob 등으로 특정 시간에 학습하고 특정시간에 예측함 (1시간 단위, 1주일 단위 등)
   - 예측한 결과를 db table에 저장하고 서버에서 이값을 활용하는 방식으로 활용가능
- **online Serving**
   - API Serving, 주문하고 바로 음식을 만들어서 서빙하는 경우와 같다.
   - 음식을 한번에 하나씩 포장해서 배송해준다.
   - online 에서 실시간 request가 올경우 response로 반환함
   - 여러주문이 들어올 경우 확장 가능한 대응방안 필요하다. 여러 request가 들어올 경우
   - 진행해야 하는 예측이 batch 불가능한 경우
   - 실시간으로 빠르게 처리해야 하는 경우 사용하는 방식
   - flask / fastapi 를 사용해서 api 서버를 직접 개발하는 방식 사용 (docker 등에 올린다.)
   - serving 라이브러리 사용
      - kubeflow 
      - bentoML : 최근 트렌드, 간단한 사용 설명 참고하기
      - seldon core 
      - cortex
      - kfserving
      - tensorlow serving
      - torch serve
- 머신러닝 모델을 개발한 후 패키지화해서 Serving 을 한다. 
- 구글 클라우드의 practitioners guide to mlops 참고할만 함.

##  Experiment, Model Management
- `머신러닝 모델 학습과정에서 생기는 설정값, 데이터, artifact 등을 모두 저장해 놓는 것을 의미한다.`
   - 기록 내용을 보기 쉽고, 모니터링 할 수 있도록 대시보드가 필요하다.
   - 제일 좋은 메트릭을 선택하는 choice 기능도 필요하다.
- 집에서 만든 요리에 대한 레시피와 유사하다.
   - 머신러닝 모델링도 여러 파라미터, 어떤 모델 구조 등으로 여러 실험을 진행하게 됨
   - 캐글에서 많은 실험을 어떻게 기록하는지와 관련있음
   - 이러한 레시피 중에서 제일 성능이 좋았던 모델을 레스토랑으로 옮김 = production
- 요리를 만들때 생기는 부산물(최종음식, 사용한 재료 등)을 모두 저장해둠
   - 머신러닝 모델 파일, feature importance 등
   - **artifact : 학습하는 과정에서 만들어지는 이미지나 모델 파일 등**
- 다양한 SaaS 가 있다.
   - Weight and Bias, Neptune 등
   - **SaaS** : Software-as-a-Service 
      - 서비스로서의 소프트웨어, 클라우드 컴퓨팅 형태
      - 클라우드 서비스 공급자로부터 종량제 방식으로 구매하는 완전한 소프트웨어 솔루션
      - 구글 독스, 마이크로소프트 오피스, 인사관리 소프트웨어, 콘텐츠 관리 시스템, 고객관리 툴 등
      - SaaS, PaaS, IaaS 
      - 범위 : 호스팅된 응용프로그램 웹,앱 / 개발도구,데이터베이스 관리,비즈니스 분석 / 운영체제 / 서버 및 저장소 / 네트워킹 방화벽, 보안 / 데이터 센터 물리적 공간, 건물
- **MLflow가 최근 트렌드**
   - **MLflow 관련 알아 볼 것 : 머신러닝 모델의 실험과 관리 해주는 프로그램**
- Research 단계에서 model management와 production 단계에서 model management를 분리해서 mlflow를 운영하는 것이 좋다.
- 어떤 모델을 선택해할까?
   - 모델 선택 예시 : Uber의 model selection rule 참고

## Feature Store
- `머신러닝 Feature 를 집계한 저장소`
   - 더 많은 머신러닝 모델들이 개발되는 과정에서 Feature 들을 Store에 저장해 놓고 필요할 때마다 사용
   - 전처리된 데이터를 저장하므로 사용할 때 편리하다.
- 요리를 할 때 반복되어 사용되는 재료들은 미리 손질을 끝내놓고 보관해놓으면 필요할 때마다 사용하는 게 효율적이다.
   - 요리에만 집중할 수 있다.
   - 여러 요리를 해야하는 경우 필요한 재료들이 중복되는 경우 더 효율적이다.
- Research 단계와 Production 단계에서 공동으로 사용할 수 있는 Feature Store를 구축하면 더 좋다.
   - 이를 위해서는 실시간 데이터 파이프라인이 사전에 필요하다. 
- Batch 단위로 쿼리를 실행하고, 특정 DB Table에 저장한다. 이 저장된 Table을 사용한다.
   - 이를 위한 클라우드 : SageMaker Feature Store, Vertex AI 등

## Data Validation
- `Research 단계와 Production 단계에서 사용한 데이터가 같은지 다른지 확인하는 과정`
   - Research 단계에서 학습 데이터의 Feature 분포와 Production 단계에서 Feature 분포를 모니터링한다.
   - 두 데이터의 Feature 분포가 유사한지 다른지 확인.
- 집에서 만든 요리의 재료와 레스토랑에서 판매하는 요리의 재료가 다르다면 요리의 품질이 달라진다.
   - 집과 레스토랑에서 사용하는 재료가 같은지 다른지 확인 해 주어야 한다.
- **Tensorflow의 data validation 사용하여 관리할 수 있다.**
- **Data drift (데이터 표류), Model drift(모델 표류), Concept drift(컨셉 표류)** 등을 관리 하는 것이 머신러닝 모델의 성능을 유지하는 것에 중요하다.
   - 데이터, 모델, 컨셉이 변화 또는 왜곡하는 현상
   - 머신러닝 모델의 성능 저하를 초래하는 입력 데이터의 변경 내용
   - 데이터 드리프트 관련 글
      - "머신러닝 활용 사업 성패는 데이터 드리프트" http://www.aitimes.com/news/articleView.html?idxno=129565
      - "AI 모델 성능을 효율적으로 높이는 방법 : 앤드류 응 교수의 데이터 중심 AI" https://medium.com/ai-networkkr/ai-%EB%AA%A8%EB%8D%B8-%EC%84%B1%EB%8A%A5%EC%9D%84-%EC%89%BD%EA%B3%A0-%EB%B9%A0%EB%A5%B4%EA%B2%8C-%EB%86%92%EC%9D%B4%EB%8A%94-%EB%B0%A9%EB%B2%95-%EC%95%A4%EB%93%9C%EB%A5%98-%EC%9D%91-%EA%B5%90%EC%88%98%EB%8B%98%EC%9D%98-%EB%8D%B0%EC%9D%B4%ED%84%B0-%EC%A4%91%EC%8B%AC%EC%9D%98-ai-6595fa054ce6
      - 앤드류 응 교수의 강의 영상 : https://www.youtube.com/watch?v=06-AZXmwHjo&t=769s
      - AI 모델의 성능을 높이기 위한 모델 중심의 개발과 데이터 중심의 개발을 체계적으로 설명함. 추후에 보면 좋은 내용.

## Continuous Training
- 머신러닝 모델의 지속적인 재학습 과정
   - 새로운 데이터가 들어온 경우
   - Metric이 떨어진 경우
   - 일정한 기간을 두고 훈련 (1주일, 매일, 매시간 등)
   - 코드가 변경된 경우
   - 재학습 요청이 있는 경우
- 레스토랑에서 판매하는 요리에 대한 고객들의 반응 떨어진다면 신선한 재료로 다시 만들어야 한다.

## GPU Infra Management
- 로컬 GPU가 있는 경우엔, 이 환경과 Production 환경을 잘 유지시킬 필요가 있다. 리소스 분배도 필요하다.
- 집과 레스토랑의 요리 도구, 인프라를 주기적으로 관리해주는 과정

## Monitoring
- Serving 환경에서 나오는 결과 데이터를 모두 저장하고, 모니터링해야 한다.
- 인프라의 지표와 모델의 로그를 구분해서 관리한다.
   - 인프라의 지표 모니터링은 Grafana 등을 사용한다.
   - 모델의 예측, 결과 등은 BI 오픈소스인 Superset, Redash, Metabase 등을 사용하거나 직접 웹을 구축한다.
- 예측값과 실제 값의 차이를 주기적으로 확인할 수 있고, 그 값을 통해 Alert를 보내주는 시스템도 필요하다.
- 레스토랑의 매출을 잘 기록해두고, 집에서 만든 요리가 실제로 레스토랑에서 얼마나 많이 팔리는지 확인하는 과정

## Auto ML
- Research 관점에서 하이퍼파라미터를 자동으로 뽑아주거나, 네트워크의 구조도 뽑아 줄 수 있다. 
   - 마이크로소프트의 NNI 훑어 볼 것
- 자동으로 음식을 만드는 과정

# 최종 요약
- MLOps는 머신러닝 모델을 개발하고 서비스하는 과정에서 발생하는 여러가지 문제점들을 효율적으로 관리하는 과정과 같다.
   - Research와 Production 파트에서 발생하는 데이터, 성능, 모델링, 재학습 등의 세부적인 업무들을 최소한의 시간으로 관리하기 위한 과정

- MLOps 구성
   - Serving : 개발한 모델을 고객에게 서비스하는 단계
      - 대표스킬 : BentoML
   - Experiment, Model Management : 모델을 학습하는 과정에서 생기는 데이터들을 저장하고 관리
      - 대표스킬 : MLflow
   - Feature store : 모델에서 사용되는 Feature들을 저장하고 관리하는 단계
   - data validation : Reasearch 단계와 Production 단계의 Feature 를 모니터링하고 관리하는 단계
      - 대표스킬 : Tensorflow의 Data Validation
   - continuous training : CI / CD / CT 를 고려한 머신러닝 모델의 재학습 단계
   - gpu infra management : 머신러닝 모델 개발에 사용되는 인프라를 주기적으로 관리하는 단계
   - monitoring : Serving 환경에서 나오는 결과 데이터를 토대로 모니터링하는 단계 
   - auto ml : 자동으로 머신러닝 모델을 개발하는 과정
      - 대표스킬 : Microsoft NNI
- MLOps 의 구성은 계속해서 변화하고 있고, 각 구성마다 유행하는 스킬도 변화한다.
- 학습방법 : 
   - 머신러닝에 대한 기초지식을 쌓은 후 MLOps 관련 강의를 토대로 큰 그림을 그린다.
   - 여러가지 문제상황에 대한 시스템을 구축해본다.
