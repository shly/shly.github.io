---
title: mergeSort
date: 2016-05-27 14:11:55
tags: 
  - 排序算法
categories:
  - 学习笔记
  - 数据结构
---
归并排序算法总结（稳定，时间复杂度n*logn）

	public void mergeSort(int[] arr, int left, int right) {
			if(left<right){
				int center = (right+left)/2;
				mergeSort(arr,left,center);
				mergeSort(arr,center+1,right);
				merge(arr,left,right,center);
			}
			
		}
		/**
		 * 将两个数组进行排序，排序前两个数组有序，排序后依然有序
		 * @param arr 要排序的数组
		 * @param left 左数组第一个元素的索引
		 * @param right 右数组最后一个元素的索引
		 * @param center 左数组最后一个元素的索引，center+1是右数组第一个元素的索引
		 */
		public void merge(int[] arr,int left,int right,int center){
	//		与待排序数组等长的临时数组
			int[] temp = new int[arr.length];
	//		右侧数组的索引
			int mid = center+1;
	//		third 中间数组的索引
			int third = left;
	//		记录左侧数组的第一个元素的索引，用于将临时数组的元素复制到原数组时
			int tmp = left;
			while(left <= center && mid <= right){
	//			从两个数组中取出小的放入中间数组
				if(arr[left]<=arr[mid]){
					temp[third++]=arr[left++];
				}else{
					temp[third++]=arr[mid++];
				}
			}
	//		剩余部分依次加入到中间数组
			while(mid<=right){
				temp[third++]= arr[mid++];
			}
			while(left<=center){
				temp[third++]= arr[left++];
			}
	//		将中间数组的内容复制回原数组
			while(tmp<=right){
				arr[tmp] = temp[tmp++];
			}
		}