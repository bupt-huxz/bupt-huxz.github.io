---
layout: post
title: 《算法》读书笔记（一）
description: 第一章 基 础
category: blog
---

## 1、递归  

编写递归代码时最重要的有一下三点。  

* 递归总有一个**最简单的情况**---方法的第一条语句总是一个包含return的条件语句。  
* 递归调用总是去尝试解决一个**规模更小**的子问题，这样递归才能收敛到最简单的情况。在下面的代码中，第四个参数和第三个参数的差值一直在缩小。
* 递归调用的父问题和尝试解决的子问题之间不应该有**交集**。在下面的代码中，两个子问题各自操作的数组部分是不同的。

二分查找的递归实现：

	public static int rank(int key, int[] a)
	{	return rank(key, a, 0, a.length - 1);	}
	
	public static int rank(int key, int[] a, int lo, int hi)
	{	//如果key存在于a[]中，它的索引不会小于lo且不会大于hi
		
		if (lo > hi) return -1;
		int mid = lo + (hi - lo)/2;
		if		(key < a[mid]) return rank(key, a, lo, mid-1);
		else if (key > a[mid]) return rank(key, a, mid+1, hi);
		else                   return mid;
	}

欧几里得算法（计算两个非负整数p和q的最大公约数）：若q是0，则最大公约数为p。否则，将p除以q得到余数r，p和q的最大公约数即为q和r的最大公约数。

	public static int gcd(int p, int q)
	{
		if (q == 0) return p;
		int r = p % q;
		return gcd(q, r);
	}


		

