---
layout: post
title: 백준 16917번 문제 풀이
date: 2021-06-09 14:33:29 +0300
img: 18.jpg
tags: Rest
---

첫번째 알고리즘 문제, 백준 16917번 문제 풀이 - 210609

***
## 0.목차
> 1. 예제 
>> 1-1. 주제 소개
>> 1-2. 문제 정의 
> 2. 어떻게 접근?
> 3. 실제 코드
> 4. 다른사람 코드
> 5. 문제점
> 6. 자료 출처

## 1.예제 
현진 치킨에서 판매하는 치킨은 양념 치킨, 후라이드 치킨, 반반 치킨으로 총 세 종류이다.반반 치킨 절반은 양념 치킨, 절반은 후라이드 치킨으로 이루어져있다. 
양념 치킨 한 마리의 가격은 A원, 후라이드 치킨 한 마리의 가격은 B원, 반반 치킨 한 마리의 가격은 C원이다.

상도는 오늘 파티를 위해 양념 치킨 최소 X마리, 후라이드 치킨 최소 Y마리를 구매하려고 한다. 반반 치킨을 두 마리 구입해 양념 치킨 하나와 후라이드 치킨 하나를 만드는 방법도 가능하다. 상도가 치킨을 구매하는 금액의 최솟값을 구해보자.

- 1 ≤ A, B, C ≤ 5,000
- 1 ≤ X, Y ≤ 100,000


### 1-1.주제 소개 
주제는 양념치킨, 후라이드치킨을 먹고싶은데 치킨을 임의의 최소수량 만큼 샀을 때, 지불할 수 있는 최솟값을 구하라는 것이다. 

### 1-2.문제 정의
여기서 키포인트는 반반치킨 1개는 후라이드치킨 0.5개, 양념치킨 0.5개다.
만약 A+B (양념치킨 1마리, 후라이드치킨 1마리 샀을때) 의 값이 반반치킨 2개를 시켰을때 가격보다 비싸면 양념치킨 1마리, 후라이드치킨 1마리를 살 필요가 없다. 
2C 를 구매하면 된다. 이부분만 이해하면 문제는 쉽게 풀릴 것이다. 
![chicken](../../../../images/chicken.jpeg)

## 2.어떻게 접근?
우선 주석으로 생각정리를 시작한다. 크게는 두가지 경우로 나뉜다. <br>
<br>
<u><span style="color:blue"> 1) A+B > 2C  이때는 반반치킨으로 승부를 본다.</span></u>
> - X>Y(양념치킨이 후라이드 치킨보다 많으면) Y개의 갯수에 맞춰서 반반치킨을 구매한다. 예를들어 양념치킨 4개, 후라이드치킨 5마리인데 반반치킨을 10마리 시켜버리면 양념치킨 5마리, 후라이드 5마리로 양념치킨 1마리가 남아버린다. 하지만  치킨을 남겼을때가 더 싸다면 남겨도 되는 조건도 걸어보자.
> - 반반치킨을 Y개의 갯수에 맞게 샀다면 나머지 양념치킨 X마리를 개별 구매해야한다. (X-Y) * A 만큼 더해주면 된다. 


<u><span style="color:blue">2) A+B < 2C  이때는 치킨을 그냥 하나씩 시킨다. </span></u>

## 3.실제코드

```java
 
 package programmers;

import java.util.Scanner;
/*
 1<= A,B,C <= 5000
 * 1<= X,Y <=100000
 *  양념치킨 A 원
 *  후라이드치킨 B 원
 *  반반치킨 한마리 C 원 
 *  
 *  ========구조 파악=================
 * 1)  (A+B) 가격이 2*C가격보다 크면 반반먼저 산다.
 * 2)  X>Y면  Y개까지만 산다
 * 3)  그리고  X-Y개를 더산다. 
 * 4)  A보다 2*C가 더싸면 (x-y)*2*C를 더하자
 * 5)  아니고 A가 더 싸면 (X-Y)*A로 사자
 * 6)  같으면 (X-Y)2*C로 사자 (그냥 치킨많을수록 조으니까)
 * ==============================
 * 
 * */

/**
 * 
 * @작성자: sue
 * @작성일 : 2021.06.08
 * @도와준사람 : 현딕
 * 
 */

public class Chicken2 {

	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);

		System.out.println("양념치킨, 후라이드, 반반치킨 가격과 양념치킨과 후라이드치킨의 최소 수량을 순서대로 입력하세요.");

		int A = sc.nextInt();
		int B = sc.nextInt();
		int C = sc.nextInt();
		int X = sc.nextInt();
		int Y = sc.nextInt();
		int sum = 0;
		int test, test1 = 0; // 반반 가격이 더 쌀때, 조건별 값을 넣어줄 변수

		// (A+B) 가격이 2*C 가격보다 크면 반반 먼저 산다.
		if ((A + B) > 2 * C) {
			// 반반 먼저 산다
			if (X > Y) {
				// X>Y 이면 Y의 갯수 *2 *C 를 곱한다. 그리고 남은 양념치킨 (X-Y)*A를 더해준다
				test = (Y * 2 * C) + ((X - Y) * A);
				// X>Y 여도 Y만큼 C 를 산 값이 더 저렴하다면 X*2*C 를 해준다
				test1 = X * 2 * C;
				if (test < test1) {
					sum = test;
				} else {
					sum = test1;
				}
			} else if (X < Y) {
				// X<Y 이면 X의 갯수 *2 *C 를 곱한다.그리고 남은 후라이드치킨 (X-Y)*B를 더해준다
				test = (X * 2 * C) + ((Y - X) * B);
				// X<Y 여도 Y만큼 C 를 산 값이 더 저렴하다면 Y*2*C 를 해준다
				test1 = Y * 2 * C;
				if (test < test1) {
					sum = test;
				} else {
					sum = test1;
				}
			} else {
				// X=Y 이면 둘중 아무거나 갯수 *2 *C 를 곱한다.
				sum = X * 2 * C;
			}
			// 두개가격을 합친것보다 반반 2개가격이 더 많이 나가면 반반을 살필요 없으므로
			// 양념과 후라이드를 개별로 산다
		} else if ((A + B) < 2 * C) {
			// 개별로 산다
			sum = (X * A) + (Y * B);
		}

		System.out.println("결과값 :" + sum);

	}
}
```

### 4. 다른사람 코드

>[깃헙주소](https://hs95blue.github.io/chicken)

### 5. 문제점

첫 알고리즘 문제다보니 시행착오가 많았다. 그리고 무작정 구글에 검색해 풀어놓은 코드를 참고해 풀고싶었다. 어디부터 만져야 하고, 뭐부터 생각해야하는지가 막막했다. 도움을 구한 결과, 주석으로 생각정리를 하고 코드를 구현해야한다고 했다. 
나는 무작정 코드를 치면서 생각을 했다. 왜냐면 그 생각의 과정이 길고 머리아프니까..하지만 설계없는 코드는 공허하다고 했다. 그리고 가독성이 떨어진다..지금은 처음이어서 생각정리 하는게 많이 어색하고 힘들다. '하다보면 늘겠지!' 란 기대감에 꾸준히 풀어보자.
- - -
