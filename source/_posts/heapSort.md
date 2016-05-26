---
title: heapSort
date: 2016-05-26 11:06:29
tags: 
  - 排序算法
categories:
  - 学习笔记
  - 数据结构
---
java堆排，记录一下。（选择排序，时间复杂度O(n*logn),不稳定排序）

	public void heapSort(int[] arr) {
			int arrLength = arr.length;
			for(int i = 0;i<arrLength-1;i++){
				int lastIndex = arrLength-1-i;
				buildMaxHeap(arr,lastIndex);
				swap(arr,0,lastIndex);
			}
		}
		public void buildMaxHeap(int[] arr,int lastIndex){
			for(int i = (lastIndex-1)/2;i>=0;i--){
				int k = i;
				while(k*2+1<=lastIndex){
					int biggerIndex = 2*k+1;
					if(biggerIndex<lastIndex){
						if(arr[biggerIndex]<arr[biggerIndex+1]){
							biggerIndex++;
						}
					}
					if(arr[k]<arr[biggerIndex]){
						swap(arr,k,biggerIndex);
						k = biggerIndex;
					}else{
						break;
					}
				}
			}
		}
其他排序算法见 https://github.com/shly/datastructure