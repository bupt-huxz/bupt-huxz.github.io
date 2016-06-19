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

## 2、定容栈

数据类型的实现

	public class FixedCapacityStackOfStrings
	{
	 	private String[] a; // stack entries
		private int N;      // size
		public FixedCapacityStackOfStrings(int cap)
		{ a = new String[cap]; }
		public boolean isEmpty() { return N == 0 ; }
		public int size() { return N; }
		public void push(String item)
		{ a[N++] = item; }
		public String pop()
		{ return a[--N]; }
	}

## 3、泛型定容栈

数据类型的实现

	public class FixedCapacityStack<Item>
	{
		private Item[] a;   //stack entries
		private int N;      //size
		public FixedCapacityStack(int cap)
		{ a = (Item[]) new Object[cap]; } //注：创建泛型数组在Java中是不允许的，                                   
										  //需类型转换
		public boolean isEmpty() { return N == 0; )
		public int size() { return N; }
		public void push(Item item)
		{ a[N++] = item; }
		public Item pop()
		{ return a[--N]; }
	}

## 4、下压(LIFO)栈（能够动态调整数组大小的实现）

	import java.util.Iterator;
	public class ResizingArrayStack<Item> implements Iterator<Item>
	{
		private Item[] a = (Item[]) new Object[1];  // 栈元素
		private int N = 0;                          // 元素数量
		public boolean isEmpty()  { return N == 0; }
		public int size()         { return N;      }
		private void resize(int max)
		{	//将栈移动到一个大小为max的新数组
			Item[] temp = (Item []) new Object[max];
			for(int i = 0; i < N; i ++ )
				temp[i] = a[i];
			a = temp;
		}
		public void push(Item item)
		{	//将元素添加到栈顶
			if (N == a.length) resize(2*a.length);
			a[N++] = item;
		}
		public Item pop()
		{	//从栈顶删除元素
			Item item = a[--N];
			a[N] = null;  // 避免对象游离
			if ( N > 0 && N == a.length/4) resize(a.length/2);
			return item;
		}
		public Iterator<Item> iterator()
		{ return new ReverseArrayIterator(); }
		private class ReverseArrayItaretor implements Iterator<Item>
		{	// 支持后进先出的迭代
			private int i = N;
			public boolean hasNext() { return i> 0;   }
			public Item next()       { return a[--i]; }
			public void remove()     {                }
		}
	}

 
			
		  	
							

		
		
		

