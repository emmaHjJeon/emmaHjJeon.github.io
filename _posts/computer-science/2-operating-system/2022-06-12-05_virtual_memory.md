---
layout: post
title: [OS] 05_Virtual Memory 
description: 
sitemap: false
hide_last_modified: false
categories: computer-science/2-operating-system
---

* toc
{:toc .large-only}

# 가상 메모리 

? Questions 
- 가상 메모리와 페이징 시스템 
- 요구 페이징과 페이지 폴트 
- MMU와 TLB 


## 가상 메모리란
    - 실제 메모리보다 많아 보이게 하는 기술 
    - 여러 프로세스를 동시 실행하는 시스템에서 메모리 용량 부족 이슈, 프로세스 메모리 영역 침범 이슈를 해결하기 위한 기술 
    
    - 프로세스는 가상 주소를 사용하면서, 실제 메모리 Read/Write 필요 시에는 물리 주소로 변환 
        - Virtual Address
        - Physical Address 

### MMU 
    : Virtual Address ==> Physical Address 로 매핑하는 HW 장치 

## 페이징 시스템 

- Paging
    : 크기가 동일한 (ex. 4KB) 페이지 단위로 가상 주소 공간과 매칭되는 물리 주소 공간을 관리하는 알고리즘 
    - 페이지 번호를 기반으로 매핑 정보를 기록하고 사용(PCB Process Page Table에 기록)
        - 각 첫 페이지의 가상주소에 매핑되는 물리주소가 PCB page table에 남아 있다. 
        - 찾고자하는 데이터가 위치한 페이지의 가상주소에 매핑된 물리주소 + 변위 => 데이터 실제 위치한 물리주소가 된다. 

- Page Table 
    : 물리 주소에 있는 페이지 번호와 해당 페이지의 첫 물리 주소 정보를 매핑한 표 
    
* 다중 단계 페이징 시스템 
    : 페이지 번호 BIT를 구분해서 CPU가 프로세스에서 접근할 때, Table을 생성하도록 하는 시스템


1. CPU가 MMU에 가상주소 요청 
2. MMU가 CPU CR3 레지스터에 있는 프로세스 페이지 테이블 메모리 주소를 읽어서 메모리에서 탐색
3. MMU가 Memory 상 페이지 테이블에서 원하는 물리주소 확인 
4. MMU가 데이터가 위치한 물리주소 접근 
5. Memory에서 CPU로 데이터 전달 

### TLB 
: 가상 메모리 접근 속도 향상을 위한 TLB(Translation Lookaside Buffer)
Memory 에 접근하는 속도는 상당히 느린데, <b>기존 구조에선 MMU가 페이지 테이블 정보를 찾고,</b> 다시 페이지 테이블로부터 데이터 위치를 찾는 과정에서 시간이 배로 드는 비효율 존재 

=> 페이지 테이블 정보를 캐쉬 형태로 저장하는 기술 -> TLB
=> TLB에 페이지 정보가 있다면, MMU가 메모리에서 직접 테이블 정보를 가져오는 시간을 절약할 수 있다. 

### 공유 메모리 IPC
    : 프로세스간 동일 물리 주소를 가리켜 공간, 메모리 할당 시간을 절약할 수 있다. 

### Demand Paging 
    - 