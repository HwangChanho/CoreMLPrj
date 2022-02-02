# CoreMLPrj

### Since...

- 기존에 추론을 수행할땐 사전에 학습된 모델을 가져와서 Accelerate나 metal performance shaders(MPSes) 같은 기존 프레임워크를 사용해서 포팅하려면 몇가지 작업이 필요했다.

- Accelerate랑 MPSes는 여전히 사용되지만 Core ML 내부에서 동작하고, Core ML이 이 내부 프레임워크중 어느것을 사용해야할지 결정해준다.

![CoreMLStructure.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e0916ae5-9f01-42a0-9fac-116bb26078c9/CoreMLStructure.png)

### 그래서 CoreML이 뭔가?

- CoreML은 코드에서 ML모델에 쉽게 접근하고 사용할 수 있게, ML 모델을 iOS에 가져와 표준 인터페이스로 감싸는 절차를 쉽게 만들어 주는 도구 묶음이다.

### 작업 흐름

> ML 작업 흐름은 **훈련(training)** 과 **추론(interface)**의 두 가지 주요 작업으로 구성된다.
> 

![CoreML_training_structure.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9e446341-8eef-41ee-9fb3-65b04571f50e/CoreML_training_structure.png)

- Core ML Tools는 Keras, turi, Caffe, scikit-learn, LibSVN, XGBoost 프레임워크를 포함하여 내부 혹은 서드파티 플러그인 프레임워크 대부분을 지원한다.
- 또한 애플은 이 패키지를 다름 프레임워크나 직접 사용할 수 있도록 모듈식으로 구성해 오픈소스로 제공한다.

![CoreML_Model_As_Code.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/62540944-812f-4d33-ba3c-67f4bbda5c3b/CoreML_Model_As_Code.png)

- 모델이 import 되면 Xcode는 모델과 모델의 입력과 출력을 감싸는 인터페이스를 생성한다.

### 학습 알고리즘

- **입력 데이터 포인트**: 이미지 분류의 경우 우리가 분류하고 싶은 분야 (ex. 동물 이미지)
- **입력에 대한 기대 출력**: 동물 이미지 분류 기준, 기대 출력은 각 이미지에 연결된 레이블 (ex. 개, 고양이등)
- **ML 알고리즘**: 입력 데이터 포인트를 의미있는 출력으로 변환하는 방법을 자동으로 학습하기 위해 사용되는 알고리즘. 이 유도된 규칙의 집합을 모델이라고 하면 훈련이라는 학습 절차를 통해 유도된다.
