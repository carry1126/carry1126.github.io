---
title: "순열- 숫자조합"
date: 2021-08-05 15:30:00 -0400
categories: algorithm
---
두번째 글로 어떤 것을 쓸까? 고민했다. Jekyll의 Minimal Mistakes theme를 이용한 카테고리 설정을 해보고 이에 대한 것을 정리해서 올려볼까했는데 구글링 검색하면 테마별로 설정도 다르고 아직은 어떻게 적용해야될지 잘 모르겠다. 헷갈려서 머리만 아픔@@! 카테고리는 포스트 글이 많아지면 적용해 보도록 해야겠다.   
현재 알고리즘을 이용한 코딩테스트를 준비해야되는데 프로그래머스에서 "완전탐색을 이용한 소수찾기"를 풀어보다가 숫자로 뽑는 부분이 막혀서 검색해보았다. 감을 잃은 것 같아서ㅜㅜ 구글링을 참고해서 순열에 대해서 정리해보았다.

# 순열(permutation)
## 서로 다른 n개의 값에서 r개를 선택해서 일렬로 나열하는 것
조합과 다르게 순서가 있다. 예를 들어서, 조합은 123, 321을 같다고 보지만 순열은 다른 것으로 인식한다.   
순열과 조합의 차이는 다음 링크를 참고하자.   
[참조] <https://widekey6.tistory.com/105>   
순열의 수를 구하는 공식은 다음과 같다.   
![image](https://user-images.githubusercontent.com/4480718/128305286-17fec9e2-3778-4b7b-8f35-52bf287b6192.png)


## 123이라는 숫자가 있을때 나올 수 있는 모든 수를 어떻게 구할 수 있을지 살펴보자
순환(recursion)을 이용해서 구할 수 있는데 순환은 다음의 조건을 만족해야한다.   
1.적어도 **basecase**(순환되지 않고 종료되는 case)가 있고 **모든 case는 basecase로 수렴**되어야 한다.   
2.암시적(implicit) 매개변수를 **명시적(explicit) 매개변수**로 바꾸어라.   
[참조] <https://codevang.tistory.com/297>   

123으로 만들수 있는 숫자의 조합은 3P1 + 3P2 + 3p3 = 3 + 6 + 6 = 15가지이다.(nPr 순열의 공식 적용)   
이것을 가지고 순환을 적용해보자.   
123의 숫자를 가지고 있는 배열을 arr, 조합된 숫자를 담을 배열을 result라고 한다면
```
for (int i = 0; i < arr.size(); i++) {
  permutation(arr, result, 0, arr.size(), i+1);
}
```
이런 식으로 호출할 수 있다.
```
public void permutation(List<Integer> arr, List<Integer> result, int begin, int end, r) {  //begin, end로 명시적 표현
  if (r == 0) {
   //basecase
    ...결과 처리...
  } 
  
  for (int i = begin; i < end; i++) {
    result.add(arr.remove(i));
    permutation(arr, result, 0, end-1, r-1);
    arr.add(i, result.remove(result.size() - 1));
  }                      
}
```
