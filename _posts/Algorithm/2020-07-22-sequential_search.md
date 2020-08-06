---
layout: post
title: "[Algorithm]순차검색, 이분검색 알고리즘(Sequential, Binary Search)"
description: >
    순차검색 - 처음부터 끝까지 차례로 탐색하는 알고리즘  
    이분검색 - 범위를 반으로 줄여가며 탐색하는 알고리즘
author: Yunmin Cho
tags: [Algorithm]
category: [Algorithm]
---  

📌 __순차 검색 알고리즘__   
리스트에서 특정한 값을 찾고자 할때, 요소의 처음부터 끝까지 확인하여 탐색하는 방법  
- 장점: 가장 단순하여 구현이 쉽고, 정렬되지 않은 리스트에도 사용 가능  
- 단점: 리스트의 길이가 길면 비효율적  

<br/>

❓ 문제: 크기가 n인 배열 S에 x가 있는가?   
- x와 같은 요소를 찾을 때까지 S에 있는 모든 요소를 차례로 검사한다.  
- 만일 해당 요소를 찾으면 S에서의 위치를 반환하고, 찾지 못하면 0을 반환한다.  

<br/>

❓ 순차검색으로 키 x를 찾기 위해서 몇 개의 요소를 검사해야 하는가?  
- 최적: 키 x의 위치에 따라 다름  
- 최악: S의 요소 개수인 n번(전체 검색)  

<br/>  

~~~c++
void sequential(int n, const keytype S[], keytype x, index& location){
    location = 1;
    while(location <= n && S[location] != x){ 
        // 아직 검사할 요소 남았으면, 키 x를 찾지 못했으면
        location++;
    }

    if(location > n){ // 키 x를 찾지 못했으면
        location = 0;
    }
}
~~~  

<br/>  
* * *  
<br/>  

📌 __이분검색 알고리즘__  
<span style="color: #F57C7C">정렬되어 있는 배열에서 특정 값을 찾고자 할 때 </span> 탐색 범위를 절반으로 줄여가며 확인하여 탐색하는 방법  

- 장점: 순차검색 알고리즘보다 탐색 속도가 훨씬 빠르다.  
- 단점: 배열이 반드시 정렬되어 있어야 한다.  

<br/>  

❓ 문제: 크기가 n인 <span style="color: #F57C7C">정렬된</span> 배열 S에 x가 있는가?  
- 배열 S의 처음과 끝값, 그 중간 값이 x보다 크면 왼쪽 절반, x보다 작으면 오른쪽 절반을 다시 처음과 끝으로 지정한다.  
- 배열 S의 크기를 계속 절반으로 줄여가며 확인하고, 해당 x값이 있으면 S에서의 위치를 반환하고, 찾지 못하면 0을 반환한다.  

<br/>

❓ 이분검색 알고리즘으로 키 x를 찾기 위해서 배열 S에 있는 항목을 몇 개나 검사해야 하는가?  
- 최적: 1번(배열의 중간 값이 키 x일 경우)  
- 최악: log n + 1 (밑이 2인 log) - 계속 검색 대상을 반씩 감소시키기 때문에  

<br/>  

~~~c++
void binsearch(int n, const keytype S[], keytype x, index& location) {
    index low, mid, high;
    low = 1; high = n;
    location = 0;
    while(low <= high && location == 0){
        mid = (low + high) / 2;
        
        if(x == S[mid])
            location = mid;  
        else if(x < S[mid])  
            high = mid - 1;  
        else
            low = mid + 1;
    }
}
~~~