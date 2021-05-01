---
title: 10. Policy based 
author: Jungi Lee
date: 2021-04-27 01:00:00 +0900
categories: [Reinforcement Learning, Single-Agent]
tags: [RL, Single-Agent]
math: true
mermaid: true
---
# 목차 
1. [Problem definition](#problem-definition)  
1. [Why? Policy-based](#why-policy-based)  
1. [Policy-based의 목표](#policy-based의-목표)  
1. [Reference](#reference)  

# Problem definition

기존 Q learning은 value-based로 $$\epsilon$$-greedy 방법을 사용하였다. policy-based는 neural network로부터 mean, variance를 얻어서 만든 distribution을 따른 action sample을 얻는 방법이다. 그렇다면 왜 policy based를 사용해야하는 가? 

# Why? Policy-based

value-based는 continuous action이 힘들다는 문제가 있다. 그리고 stochastic한 policy에 policy-based가 좋다. 예를 들어 가위바위로를 할 경우 각 action이 이길 확률은 $$\frac{1}{3}$$이기 때문에 stochastic해야한다. 

# Policy-based의 목표

Policy-based의 목표는 Expected return을 최대화하는 것에 있다.

$$G_0 = R_0 + \gamma R_1 + \gamma^2 R_2 + \cdots$$

$$J = \underset{s_0,a_0,s_1,a_1, \dots}{E}[G_0] = \int_{s_0,a_0,s_1,a_1, \dots} G_0 P_{\theta}(s_0,a_0,s_1,a_1, \dots) \,ds_0,a_0,s_1,a_1,\dots$$   
$$= \int_{\tau} G_0 P_{\theta}(\tau) \,d\tau$$

where $$\tau = s_0,a_0,s_1,a_1 \dots$$

$$\theta \gets \theta + \alpha \nabla_{\theta}J_{\theta}$$

# Reference
1. [혁펜하임 유투브][혁펜하임 유투브]  

[혁펜하임 유투브]: https://www.youtube.com/watch?v=cvctS4xWSaU&list=PL_iJu012NOxehE8fdF9me4TLfbdv3ZW8g  


