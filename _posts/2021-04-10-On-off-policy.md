---
title: 5. On/off-policy 
author: Jungi Lee
date: 2021-04-10 21:40:00 +0900
categories: [Reinforcement Learning, Single-Agent]
tags: [RL, Single-Agent]
math: true
mermaid: true
---


# 목차  
1. [Behavior policy and target policy](#behavior-policy-and-target-policy)  
1. [On policy](#on-policy)
1. [Off policy](#off-policy)
1. [Off policy의 장점](#off-policy의-장점)
1. [Reference](#reference)

# Behavior policy and target policy 
On policy와 off policy는 behavior policy와 target policy가 같은지 다른지에 따라 결정이된다. 
Behavior policy는 현재 action을 고르기 위해서 사용된 policy이다.  
Target policy는 TD target을 만들기 위해서 사용된 policy이다.

# On policy  
On poliyc는 bahavior policy와 target policy가 같은 경우이다. SARSA는 on policy이다.  
$$Q(s_t, a_t) = \int_{s_{t+1},a_{t+1}} (R_t + \gamma Q(s_{t+1},a_{t+1})) P(a_{t+1} \mid s_{t+1}) P(s_{t+1} \mid s_t, a_t) \, ds_{t+1},a_{t+1} $$  
$$ \approx (1-\alpha) \bar{Q}_{N-1} + \alpha (R^N_t + \gamma Q(s^N_{t+1},a^N_{t+1}))$$  
SARSA는 현재 action을 선택하기 위해서 $$Q(s_t, a_t)$$를 사용한다. 그리고 업데이트를 하기 위해서 사용된 policy는 $$Q(s_{t+1}, a_{t+1})$$를 사용한다.  
Behavior policy와 target policy 둘다 Q function에서 가져와 사용한다. 그러므로 On-policy이다.  

# Off policy  
Off policy만 제대로 이해한다면 on policy, behavior policy, target policy와 같은 개념도 쉽게 이해할 수 있을 것이다.  
Q-learning은 off policy로 target policy와 behavior policy가 다르다.  
Q-learning의 behavior policy는 $$\epsilon$$-greedy 방식이다.  
Q-learning의 target policy는 $$P(a_{t+1} \mid s_{t+1}) = \delta(a_t - a^*_t)$$이므로 $$a^*_{t+1} = \underset{a_{t+1}}{\operatorname{argmax}}Q(s_{t+1}, a_{t+1})$$이다. 
Q-learning의 TD target은 $$R_t + \gamma \underset{a_{t+1}} Q(s^N_{t+1}, a^N_{t+1})$$으로 이전에 $$\epsilon$$-greedy에 의해 $$a_{t+1}$$를 선택하여 episode를 실행한다고 해도 max값으로 TD target을 만들기 때문에 episode를 실행하기 위해 만들어진 행동과 TD target을 위해 선택된 행동이 다르다.  
$$\int_{s_{t+1},a_{t+1}} (R_t + \gamma Q(s_{t+1}, a_{t+1})) \delta(a_{t+1} - a^*_{t+1})P(s_{t+1} \mid s_t, a_t) \, ds_{t+1},a_{t+1}$$
$$=\int_{s_{t+1}} (R_t + \gamma \underset{a_{t+1}}{\operatorname{max}} Q(s_{t+1}, a_{t+1}) P(s_{t+1} \mid s_t,a_t) \, ds_{t+1}$$  

# Off policy의 장점  
1. 사람이나 다른 agent의 target policy를 사용 가능하다.  
1. 실컷 탐험하면서 Optimal policy로 sample(TD target을 얻는다.)  
1. 재평가 가능  
	- 이 말이 가장 이해가 안됬는 데 재평가가 가능하다는 말은 이전에 만든 episode를 다시 학습에 사용가능하다는 의미이다.
	- SARSA는 현재 $$Q(s_t,a_t)$$는 학습으로 인해 이전에 만든 episode의 $$Q(s_t, a_t)$$와 크게 달라져 있다. 그래서 epsiode를 학습에 다시 사용할 수 없다.(episode의 행동을 할 확률 분포가 달라짐)  

# Reference
1. [혁펜하임 유투브][혁펜하임 유투브]

[혁펜하임 유투브]: https://www.youtube.com/watch?v=cvctS4xWSaU&list=PL_iJu012NOxehE8fdF9me4TLfbdv3ZW8g  
