# Scipy and Numpy

## Chapter 1 Introduction 

NumPy specializes in numerical processing through multi-dimensional ndarrays, where the arrays allow element-by-element operations. 


## Chapter 2 Numpy

	import numpy as np
	# create an array with 10^7 elements
	arr = np.arrange(1e7)
	# 转换成矩阵
	larr = arr.tolist()
	
	def list_times(alist, scalar):
		for i val in emumerate(alist):
			alist[i] = val * scalar
		return alist
