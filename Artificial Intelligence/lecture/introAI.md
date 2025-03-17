IntroAI
=======

ai란 인간 수준의 지능인가?
-----------------------

### ai가 무엇을 할 수 있고 무엇을 못하는가? (인간에 비해서)
먼저, 컴퓨터 비전이 있다.

2015년은 컴퓨터비전에 있어 마일스톤한 년도였다.
- 알렉스넷, VGG, 구글넷, deep residual net

cnn은 계층적 표현법을 배운다?

deep reinforcemnet learning
- 아타리게임
- 단순히 뉴럴네트워크를 사용하였음.
- 마지막 4개의 프레임을 입력으로, 3-layer NN을 거쳐, 키스트로크

style transfer, complete drawing from sketch, image completion, image manipulation, drawing from text description

GPT-3, chatgpt

#### 데이터는 ai의 발전을 방해할 수 있다.
- 훈련용 데이터는 2026년에 고갈될 것이다.
  - chinchilla scaling law에 따르면, 지금 속도대로 GPT5같은 모델이 계속된다면, 대략 60~100조의 데이터 토큰을 필요로 할 것이다. 이는 기존의 높은 품질의 텍스트 데이터보다 10조에서 20조 정도 초과하는 수치이다.
- 데이터는 머신 러닝 모델을 스케일링 업하는데에 있어 병목상태이다?
- 사전훈련된 모델의 성능이 평준화될것이다.

#### LLM과 생성형 ai의 한계
1. 데이터를 만들기가 쉽다. => 저품질의 데이터가 범람한다. => 훈련에 사용할 좋은 데이터를 필터링하는 데에 비용이 발생한다.
2. 환경적 이슈
3. AI 환각
4. 정보를 업데이트하고, 삭제하기의 어려움.
5. 보안, 권한 이슈. => 각 회사와 단체들은 자체적으로 ai를 갖춰야 함.

how to implemnet artificial intelligence?

AI 문제의 두 종류.
- computational challenge
- information challenge

ai에는 computation(time/memory)와 information(data)라는 자원이 필요하다.

소프트웨어의 발전.
현실의 일에 알고리즘을 적용하여 해결함. 또는 정답을 가져옴.

ai의 발전.
현실의 일, 또는 데이터에 모델링을 하여, 모델을 만들어 내고, 추론하여 해결함.

모델링과 알고리즘
- Separate what to compute (modeling) from how to compute it (algorithms) => Advantage: division of labor

머신러닝의 단계(또는 종류)
1. reflex
2. states
3. variables
4. logic

Reflex-based models
- 예시: 선형분류기, 딥 뉴럴네트워크
- 적용 예: 감정 분석.
  - 입력: 영화의 리뷰
  - 출력: 감정
  - 감정 분석 모델
    - 입력: x, a document or sentences
    - output: f(x), a simple function of x

state-based Models
문제 해결 과정은 그래프를 지나는 경로로 표현될 수 있다.

다음과 같은 것들이 있다.
search problem, markov decision processes, adversarial games

variables
CSP