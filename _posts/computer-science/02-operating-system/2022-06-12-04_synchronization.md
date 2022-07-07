---
layout: post
title: [OS] 04_Synchronization 
description: 
sitemap: false
hide_last_modified: false
categories: computer-science/2-operating-system
---

* toc
{:toc .large-only}

# 동기화


## 동기화 이슈 


## 동기화 이슈 해결방법 

### 1. Mutex(Mutual Exclusion) 
: 한 쓰레드가 공유 변수를 변경할 때 다른 쓰레드가 동시 접근하지 못하도록 배제 
- Critical Resource: 동시 접속 되는 공간  
- Critical Section: 동시 접근 배체 공간 


### 2. Semaphore 
- Mutex는 Critical Section에 1 쓰레드만 접근 반면, 
- Semahore는 Critical Sectio에 n 쓰레드 접근 가능 
    - Counter를 둬서 접근 가능 쓰레드 수를 제어


## 교착 상태와 기아 상태

### Dead Lock
: 2 이상의 Job이 상대 JobEnd만을 기다려서 무한 대기가 발생하고 다음 단계로 진행하지 못하는 현상 

- 멀티 프로세스와 쓰레드에서 모두 일어날 수 있음 
- 배치 처리 시스템에서는 일어나지 않음 

### Starvation 
: 특정 프로세스가 우선순위가 낮아 자원 할당을 못 받는 현상 

- Deadlock 과 Starvation 
    - 공통: 공동 자원 점유 요청 시 발생 
    - 차이: Deadlock은 특정 Job이 무한 자원 할당이 안되는 현상, Starvation은 부족한 자원 점유를 위한 경쟁 현상을 말함 

