# REACT: SYNERGIZING REASONING AND ACTING IN LANGUAGE MODELS

https://doi.org/10.48550/arXiv.2210.03629

## abstract
기존의 LLM 연구는 추론과 행동을 별도로 연구해왔다. 본 논문에서는 이를 결합하여 LLM이 추론과 행동을 동시에 하도록 하는 ReAct 프레임 워크를 제안한다. 

LLM이 추론 과정과 행동 지정(task-specific actions)을 교차(interleaved)하여 생성하는 방법을 탐구하며, 이를 통해 더욱 강력한 시스템을 구축하고자 한다. 이 접근법에서는 **추론 과정(reasoning traces)**을 통해 모델이 내부적으로 사고를 추적하고, 계획을 업데이트하며, 외부 환경과 상호작용하는 방식을 지원한다. 한편, **행동(action)**은 모델이 외부 지식 기반(예: 위키피디아 API)이나 실제 환경과 상호작용할 수 있도록 돕는다.

추론에서 발생하는 환각(hallucination)과 오류(error propagation)의 문제를 해결한다. 이는 모델이 위키피디아 API와 상호작용하여 정확한 정보에 접근할 수 있도록 하고, 기존 체인-오브-생각보다 더 해석 가능성이 높은(task-solving) 추론 과정을 생성하기 때문이다.

또한 ALFWorld 및 WebShop이라는 두 가지 상호작용 기반 작업(interactive task)에서도, ReAct는 모방 학습(imitation learning) 및 강화 학습(reinforcement learning) 기반 방법보다 각각 34%, 10% 더 높은 성공률을 기록하였다.

## 네가지 모델 비교
```
1. Standard (기본 방식) - LLM이 단순히 정답을 추론하여 출력.
2. Chain-of-thought (CoT, 추론 전용) - 단계적 사고 과정을 수행하지만, 환경과 상호작용하지 않음.
3. Act-only (행동 전용) - 단순한 액션 수행만 진행.
4. ReAct (추론 + 행동 결합) - 사고(thinking)와 행동(acting)을 결합하여 보다 효과적인 문제 해결 가능.
```

![what can do ReAct](LLM_agent_example_ReAct.png)

## 기존 연구들의 한계
### CoT(Chain-of-Thought)의 한계
내부적으로 사고를 생성하지만, 환경과 상호작용할 수 없음 → **외부 정보 업데이트 불가**
환각(hallucination) 및 오류 전파(error propagation) 문제 발생

### 기존 연구들이 다룬 방식
멀티모달 데이터를 텍스트로 변환 → 언어 모델로 행동(action) 예측 → 컨트롤러(controller)로 실행
그러나, 고수준 목표(high-level goal)를 추론하거나, 작업 기억(working memory)을 유지하는 기능이 부족함
기존 연구들은 "추론과 행동을 결합하는 방법"에 대한 연구가 부족

## ReAct의 차별점 
추론(reasoning)과 행동(acting)을 결합

기존 모델들이 추론만 하거나 행동만 하는 것과 달리, ReAct는 두 가지를 동시에 수행

환경과 인터랙션하여 정보 업데이트 가능 (ex: Wikipedia와 상호작용하여 최신 정보 반영)

기존 방법들은 정적인 사고를 하지만, ReAct는 상황에 맞춰 동적으로 사고(reasoning) 조정 가능
따라서, 보다 현실적이고 강건한(task-resilient) AI 모델 구축 가능

## 4가지 벤치마크를 활용한 테스트
ReAct와 기존의 모델의 성능을 이하 4 종류의 벤치마크로 테스트
```질문 응답 (HotPotQA, Yang et al., 2018)
사실 검증 (Fever, Thorne et al., 2018)
텍스트 기반 게임 (ALFWorld, Shridhar et al., 2020b)
웹 페이지 탐색 (WebShop, Yao et al., 2022)
```
가장 뛰어난 성능을 보인 것은 ReAct와 CoT를 결합하는 방식이다.

내부 지시과 외부 지식 동시에 활용 가능하다는 장점 존재

적은 학습량으로도 강화 학습(reinforcement learning) 및 모방 학습(imitation learning) 기반 방법을 능가하는 성능을 보임