---
layout: post
title: 백준 16917번 문제 풀이
date: 2021-06-09 14:33:29 +0300
img: 18.jpg
tags: Rest
---


<script src="https://gist.github.com/RAMA4368/5b184a52bc37c2bcbc6373362caae7d6.js"></script>

- - -


<pre>
<```
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
</pre>
