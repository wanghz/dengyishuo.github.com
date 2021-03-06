---
author: admin
comments: true
date: 2011-08-27 21:50:59
layout: post
slug: matrix-operations
title: R与矩阵运算总结
wordpress_id: 814
categories:
- R&amp;数据艺术
tags:
- r
- 总结
- 矩阵运算
---

# 1 矩阵基本操作




## 1.1创建向量


**R**里面有多种方法来创建向量（Vector），最简单的是用函数**c()**。例如：

**>X=c(1,2,3,4)**

**>X**

**[1] 1 2 3 4**

当然，还有别的方法。例如：

**>X=1:4**

**>X**

**[1] 1 2 3 4**

还有**seq()**函数。例如：

**> X=seq(1,4,length=4)**

**> X**

**[1] 1 2 3 4**

注意一点，**R**中的向量默认为列向量，如果要得到行向量需要对其进行转置。


## 1.2创建矩阵


**R**中创建矩阵的方法也有很多。大致分为直接创建和由其它格式转换两种方法。


### 1.2.1直接创建矩阵


最简单的直接创建矩阵的方法是用**matrix()**函数，**matrix()**函数的使用方法如下：

**> args(matrix)**

**function (data = NA, nrow = 1, ncol = 1, byrow = FALSE, dimnames = NULL) **

**NULL**

其中，**data**参数输入的为矩阵的元素，不能为空；**nrow**参数输入的是矩阵的行数，默认为1；**ncol**参数输入的是矩阵的列数，默认为1；**byrow**参数控制矩阵元素的排列方式，**TRUE**表示按行排列，**FALSE**表示按列排列，默认为**FALSE**；**dimnames**参数输入矩阵的行名和列名，可以不输入，系统默认为**NULL**。例如：

**> matrix(1:6,nrow=2,ncol=3,byrow=FALSE)**

**      [,1]  [,2]  [,3]**

**[1,]    1    3    5**

**[2,]    2    4    6**

改变矩阵的行数和列数：

**> matrix(1:6,nrow=3,ncol=2,byrow=FALSE)**

**     [,1]   [,2]**

**[1,]    1    4**

**[2,]    2    5**

**[3,]    3    6**

改变**byrow**参数：

**> matrix(1:6,nrow=3,ncol=2,byrow=T)**

**     [,1]   [,2]**

**[1,]    1    2**

**[2,]    3    4**

**[3,]    5    6**

设定矩阵的行名和列名：

**> matrix(1:6,nrow=3,ncol=2,byrow=T,dimnames=list(c("A","B","C"),c("boy","girl")))**

**   boy  girl**

**A   1    2**

**B   3    4**

**C   5    6**


### 1.2.2 由其它格式转换


也可以由其它格式的数据转换为矩阵，此时需要用到函数**as.matrix()**。


## 1.3 查看和改变矩阵的维数


矩阵有两个维数，即行维数和列维数。在**R**中查看矩阵的行维数和列维数可以用函数**dim()**。例如：

**> X=matrix(1:12,ncol=3,nrow=4)**

**> X**

**     [,1] [,2] [,3]**

**[1,]    1    5    9**

**[2,]    2    6   10**

**[3,]    3    7   11**

**[4,]    4    8   12**

**> dim(X)**

**[1] 4 3**

只返回行维数：

**> dim(X)[1]**

**[1] 4**

也可以用函数**nrow()**

**> nrow(X)**

**[1] 4**

只返回列维数：

**> dim(X)[2]**

**[1] 3**

也可以用函数**ncol():**

**> ncol(X)**

**[1] 3**

同时，函数**dim()**也可以改变矩阵的维数。例如：

**> dim(X)=c(2,6)**

**> X**

**     [,1]   [,2]  [,3]   [,4]  [,5]  [,6]**

**[1,]    1    3    5    7    9   11**

**[2,]    2    4    6    8   10   12**


## 1.4矩阵行列的名称


查看矩阵的行名和列名分别用函数**rownames()**和函数**colnames()**。例如：

> **X=matrix(1:6,nrow=3,ncol=2,byrow=T,dimnames=list(c("A","B","C"),c("boy","girl")))**

**> X**

**  boy girl**

**A   1    2**

**B   3    4**

**C   5    6**

查看矩阵的行名：

**> rownames(X)**

**[1] "A" "B" "C"**

查看矩阵的列名：

**> colnames(X)**

**[1] "boy"  "girl"**

同时也可以改变矩阵的行名和列名，比如：

**>  rownames(X)=c("E","F","G")**

**> X**

**  boy girl**

**E   1    2**

**F   3    4**

**G   5    6**

**> colnames(X)=c("man","woman")**

**> X**

**  man woman**

**E   1     2**

**F   3     4**

**G   5     6**


## 1.5 矩阵元素的查看及其重新赋值


查看矩阵的某个特定元素，只需要知道该元素的行坐标和列坐标即可，例如：

**> X=matrix(1:12,nrow=4,ncol=3)**

**> X**

**     [,1] [,2] [,3]**

**[1,]    1    5    9**

**[2,]    2    6   10**

**[3,]    3    7   11**

**[4,]    4    8   12**

查看位于矩阵第二行、第三列的元素：

**> X[2,3]**

**[1] 10**

也可以重新对矩阵的元素进行赋值，将矩阵第二行、第三列的元素替换为0：

**> X[2,3]=0**

**> X**

**     [,1] [,2] [,3]**

**[1,]    1    5    9**

**[2,]    2    6    0**

**[3,]    3    7   11**

**[4,]    4    8   12**

**R**中有一个**diag()**函数可以返回矩阵的全部对角元素：

**> X=matrix(1:9,ncol=3,nrow=3)**

**> X**

**     [,1]   [,2]   [,3]**

**[1,]    1    4    7**

**[2,]    2    5    8**

**[3,]    3    6    9**

**> diag(X)**

**[1] 1 5 9**

当然也可以对对角元素进行重新赋值：

**> diag(X)=c(0,0,1)**

**> X**

**     [,1] [,2] [,3]**

**[1,]    0    4    7**

**[2,]    2    0    8**

**[3,]    3    6    1**

当操作对象不是对称矩阵时，**diag()**也可以进行操作。

**> X=matrix(1:12,nrow=4,ncol=3)**

**> X**

**     [,1] [,2] [,3]**

**[1,]    1    5    9**

**[2,]    2    6   10**

**[3,]    3    7   11**

**[4,]    4    8   12**

**> diag(X)**

**[1]  1  6  11**

**diag()**函数还能用来生成对角矩阵：

**> diag(c(1,2,3))**

**     [,1] [,2] [,3]**

**[1,]    1    0    0**

**[2,]    0    2    0**

**[3,]    0    0    3**

也可以生成单位对角矩阵：

**> diag(3)**

**     [,1] [,2] [,3]**

**[1,]    1    0    0**

**[2,]    0    1    0**

**[3,]    0    0    1**

**> diag(4)**

**     [,1] [,2] [,3] [,4]**

**[1,]    1    0    0    0**

**[2,]    0    1    0    0**

**[3,]    0    0    1    0**

**[4,]    0    0    0    1**

查看矩阵的上三角部分：在**R**中查看矩阵的上三角和下三角部分很简单。可以通过**lower.tri()**和**upper.tir()**来实现：****

**> args(lower.tri)**

**function (x, diag = FALSE) **

**NULL**

**> args(upper.tri)**

**function (x, diag = FALSE) **

**NULL**

查看上三角：

**> X=matrix(1:12,nrow=4,ncol=3)**

**> X**

**     [,1] [,2] [,3]**

**[1,]    1    5    9**

**[2,]    2    6   10**

**[3,]    3    7   11**

**[4,]    4    8   12**

**> X[lower.tri(X)]**

**[1]  2  3  4  7  8 12**

改变赋值：

**> X[lower.tri(X)]=0**

**> X**

**     [,1] [,2] [,3]**

**[1,]    1    5    9**

**[2,]    0    6   10**

**[3,]    0    0   11**

**[4,]    0    0    0**


# 2 矩阵计算




## 2.1矩阵转置


**R**中矩阵的转置可以用**t()**函数完成，例如：

**> X=matrix(1:12,nrow=4,ncol=3)**

**> X**

**     [,1] [,2] [,3]**

**[1,]    1    5    9**

**[2,]    2    6   10**

**[3,]    3    7   11**

**[4,]    4    8   12**

**> t(X)**

** [,1] [,2] [,3] [,4]**

**[1,]    1    2    3    4**

**[2,]    5    6    7    8**

**[3,]    9   10   11   12**


## 2.2矩阵的行和与列和及行平均值和列均值


在**R**中很容易计算一个矩阵的各行和和各列和以及各行的平均值和各列的平均值。例如：

**> A=matrix(1:12,3,4)**

**> A**

**     [,1] [,2] [,3] [,4]**

**[1,]    1    4    7   10**

**[2,]    2    5    8   11**

**[3,]    3    6    9   12**

**> rowSums(A)**

**[1] 22 26 30**

**> rowMeans(A)**

**[1] 5.5 6.5 7.5**

**> colSums(A)**

**[1]  6 15 24 33**

**> colMeans(A)**

**[1]  2  5  8 11**


## 2.3行列式的值


**R**中的函数**det()**将计算方阵**A**的行列式。例如：

**> X=matrix(rnorm(9),nrow=3,ncol=3)**

**> X**

**            [,1]       [,2]       [,3]**

**[1,]  0.05810412 -1.2992698  0.5630315**

**[2,] -0.28070583  0.1958623 -1.8202283**

**[3,]  0.83691209  0.4411497  1.0014306**

**> det(X)**

**[1] 1.510076**


## 2.4矩阵相加减


矩阵元素的相加减是指维数相同的矩阵，处于同行和同列的位置的元素进行加减。实现这个功能用“**＋**”，“**－**”即可。例如：

**> A=B=matrix(1:12,nrow=3,ncol=4)**

**> A+B**

**     [,1] [,2] [,3] [,4]**

**[1,]    2    8   14   20**

**[2,]    4   10   16   22**

**[3,]    6   12   18   24**

**> A-B**

**     [,1] [,2] [,3] [,4]**

**[1,]    0    0    0    0**

**[2,]    0    0    0    0**

**[3,]    0    0    0    0**


## 2.5矩阵的数乘


矩阵的数乘是指一个常数与一个矩阵相乘。设**A**为**m****×****n**矩阵，**c****≠****0**，在**R**中求**cA**的值，可以用符号“*”。例如：

**> c=2**

**> A=matrix(1:12,nrow=3,ncol=4)**

**> A**

**     [,1] [,2] [,3] [,4]**

**[1,]    1    4    7   10**

**[2,]    2    5    8   11**

**[3,]    3    6    9   12**

**> c*A**

**     [,1] [,2] [,3] [,4]**

**[1,]    2    8   14   20**

**[2,]    4   10   16   22**

**[3,]    6   12   18   24**

结果矩阵与原矩阵的所有相应元素都差一个常数**c**。


## 2.6矩阵相乘




### 2.6.1矩阵的乘法


**A****为****m****×****n**矩阵，**B**为**_n_****_×_****_k_**矩阵，在**R**中求**AB**，可以符号“**%*%****”**。例如：

**> A=matrix(1:12,nrow=3,ncol=4)**

**> B=matrix(1:12,nrow=4,ncol=3)**

**> A%*%B**

**     ****[,1] [,2] [,3]**

**[1,]   70  158  246**

**[2,]   80  184  288**

**[3,]   90  210  330**

注意**BA**无意义，因其不符合矩阵的相乘规则。

若**A**为**n****×****m**矩阵，**B**为**_n_****_×_****_k_**矩阵，在**R**中求**A’B****：******

**> A=matrix(1:12,nrow=4,ncol=3)**

**> B=matrix(1:12,nrow=4,ncol=3)**

**> t(A)%*%B**

**     [,1] [,2] [,3]**

**[1,]   30   70  110**

**[2,]   70  174  278**

**[3,]  110  278  446**

也可以用函数**crossprod()**计算**A’B**：

**> crossprod(A,B)**

**     [,1] [,2] [,3]**

**[1,]   30   70  110**

**[2,]   70  174  278**

**[3,]  110  278  446**


### 2.6.2矩阵的Kronecker积


**n****×m**矩阵**A**和**h****×k**矩阵**B**的Kronecker积是一个**nh****×mk**维矩阵，公式为：

**              a­11B ****… a1nB**

**Am****×n****×****Bh****×k=     ****…     ****…**

**               am1B ****… amnB   mh****×nk**

在**R**中Kronecker积可以用函数kronecher()来计算。例如：

**> A=matrix(1:4,2,2)**

**> A**

**     [,1] [,2]**

**[1,]    1    3**

**[2,]    2    4**

**> B=matrix(rep(1,4),2,2)**

**> B**

**     [,1] [,2]**

**[1,]    1    1**

**[2,]    1    1**

**> kronecker(A,B)**

**     [,1] [,2] [,3] [,4]**

**[1,]    1    1    3    3**

**[2,]    1    1    3    3**

**[3,]    2    2    4    4**

**[4,]    2    2    4    4**


## 2.7矩阵的伴随矩阵


求矩阵**A**的伴随矩阵可以用**LoopAnalyst**包中的函数**make.adjoint()**函数。例如：****

**>install.packages("LoopAnalyst")**

**> A=matrix(1:12,nrow=3,ncol=4)**

**> A**

**     [,1] [,2] [,3] [,4]**

**[1,]    1    4    7   10**

**[2,]    2    5    8   11**

**[3,]    3    6    9   12**

**> make.adjoint(A)**

**     [,1] [,2] [,3]**

**[1,]   -3    6   -3**

**[2,]    6  -12    6**

**[3,]   -3    6   -3**


## 2.8矩阵的逆和广义逆




### 2.8.1矩阵的逆


矩阵**A**的逆**A-1**可以用函数**solve()**，例如：

**> A=matrix(rnorm(9),nrow=3,ncol=3)**

**> A**

**           [,1]       [,2]        [,3]**

**[1,] -0.2915845  0.2831544  0.94493154**

**[2,] -1.6494678  0.6999185 -0.06292334**

**[3,] -0.7224015 -0.3906971  0.44799963**

**> solve(A)**

**          [,1]       [,2]       [,3]**

**[1,] 0.2359821 -0.4050650 -0.5546321**

**[2,] 0.6405592  0.4507583 -1.2877720**

**[3,] 0.9391490 -0.2600663  0.2147417**

验证**AA-1=1****：**

**> A%*%solve(A)**

**              [,1]         [,2]          [,3]**

**[1,]  1.000000e+00 8.433738e-17 -1.341700e-18**

**[2,]  1.216339e-17 1.000000e+00 -4.667152e-17**

**[3,] -2.203641e-17 4.283954e-17  1.000000e+00**

用**round**函数可以更好的得到结果：

**> round(A%*%solve(A))**

**     [,1] [,2] [,3]**

**[1,]    1    0    0**

**[2,]    0    1    0**

**[3,]    0    0    1**

**solve()**函数也可以用来求解方程组**ax=b****。**


### 2.8.2矩阵的广义逆（Moore-Penrose）


并非所有的矩阵都有逆，但是所有的矩阵都可有广义逆。**n****×m**矩阵**A+**是矩阵**A**的**Moore-Penrose**逆，如果它满足下列条件：****

**AA+A=A**

**A+AA+=A+**

**(AA+)T=AA+**

**(A+A)T=A+A**

**R**中**MASS**包中的**ginv()**函数可以计算矩阵的**Moore-Penrose**逆。例如：

**> library(MASS)**

**> A=matrix(1:12,nrow=3,ncol=4)**

**> A**

**     [,1] [,2] [,3] [,4]**

**[1,]    1    4    7   10**

**[2,]    2    5    8   11**

**[3,]    3    6    9   12**

**> solve(A)**

**Error in solve.default(A) : only square matrices can be inverted**

**> ginv(A)**

**             [,1]        [,2]        [,3]**

**[1,] -0.483333333 -0.03333333  0.41666667**

**[2,] -0.244444444 -0.01111111  0.22222222**

**[3,] -0.005555556  0.01111111  0.02777778**

**[4,]  0.233333333  0.03333333 -0.16666667**

验证性质①：

**> A%*%ginv(A)%*%A**

**     [,1] [,2] [,3] [,4]**

**[1,]    1    4    7   10**

**[2,]    2    5    8   11**

**[3,]    3    6    9   12**

**> A**

**     [,1] [,2] [,3] [,4]**

**[1,]    1    4    7   10**

**[2,]    2    5    8   11**

**[3,]    3    6    9   12**

验证性质②：

**> ginv(A)%*%A%*%ginv(A)**

**             [,1]        [,2]        [,3]**

**[1,] -0.483333333 -0.03333333  0.41666667**

**[2,] -0.244444444 -0.01111111  0.22222222**

**[3,] -0.005555556  0.01111111  0.02777778**

**[4,]  0.233333333  0.03333333 -0.16666667**

**> ginv(A)**

**             [,1]        [,2]        [,3]**

**[1,] -0.483333333 -0.03333333  0.41666667**

**[2,] -0.244444444 -0.01111111  0.22222222**

**[3,] -0.005555556  0.01111111  0.02777778**

**[4,]  0.233333333  0.03333333 -0.16666667**

验证性质③：

**> A%*%ginv(A)**

**           [,1]      [,2]       [,3]**

**[1,]  0.8333333 0.3333333 -0.1666667**

**[2,]  0.3333333 0.3333333  0.3333333**

**[3,] -0.1666667 0.3333333  0.8333333**

**> t(A%*%ginv(A))**

**           [,1]      [,2]       [,3]**

**[1,]  0.8333333 0.3333333 -0.1666667**

**[2,]  0.3333333 0.3333333  0.3333333**

**[3,] -0.1666667 0.3333333  0.8333333**

验证性质④：

**> ginv(A)%*%A**

**     [,1] [,2] [,3] [,4]**

**[1,]  0.7  0.4  0.1 -0.2**

**[2,]  0.4  0.3  0.2  0.1**

**[3,]  0.1  0.2  0.3  0.4**

**[4,] -0.2  0.1  0.4  0.7**

**> t(ginv(A)%*%A)**

**     [,1] [,2] [,3] [,4]**

**[1,]  0.7  0.4  0.1 -0.2**

**[2,]  0.4  0.3  0.2  0.1**

**[3,]  0.1  0.2  0.3  0.4**

**[4,] -0.2  0.1  0.4  0.7**

也可以不必如此麻烦来验证性质③和④，因为③和④只是表明**AA+**和**A+A**是对称矩阵。


### 2.8.3 X’X的逆


很多时候，我们需要计算形如X’X的逆。这很容易实现，例如：

**> x=matrix(rnorm(9),ncol=3,nrow=3)**

**> x**

**           [,1]        [,2]        [,3]**

**[1,] -0.1806586 -0.76340512 0.002652331**

**[2,] -1.8018584  0.04467943 1.416332187**

**[3,]  1.2785359 -1.31653513 0.180653002**

**> solve(crossprod(x))**

**          [,1]      [,2]     [,3]**

**[1,] 1.2181837 0.9664576 1.470940**

**[2,] 0.9664576 1.2010110 1.204599**

**[3,] 1.4709402 1.2045986 2.269921**

R中的**strucchange**包中的函数**solveCrossprod()**也可完成：****

**> args(solveCrossprod)**

**function (X, method = c("qr", "chol", "solve")) **

**NULL**

**> solveCrossprod(x,method="qr")**

**          [,1]      [,2]     [,3]**

**[1,] 1.2181837 0.9664576 1.470940**

**[2,] 0.9664576 1.2010110 1.204599**

**[3,] 1.4709402 1.2045986 2.269921**

**> solveCrossprod(x,method="chol")**

**          [,1]      [,2]     [,3]**

**[1,] 1.2181837 0.9664576 1.470940**

**[2,] 0.9664576 1.2010110 1.204599**

**[3,] 1.4709402 1.2045986 2.269921**

**> solveCrossprod(x,method="solve")**

**          ****[,1]      [,2]     [,3]**

**[1,] 1.2181837 0.9664576 1.470940**

**[2,] 0.9664576 1.2010110 1.204599**

**[3,] 1.4709402 1.2045986 2.269921**


## 2.9矩阵的特征值和特征向量


可以通过对矩阵**A**进行谱分解来得到矩阵的特征值和特征向量。矩阵**A**的谱分解如下：**A=U****Λ****U’**，其中**U**的列为**A**的特征值所对应的特征向量，在**R**中可以用**eigen()**函数得到**U**和**Λ**。例如：

**> args(eigen)**

**function (x, symmetric, only.values = FALSE, EISPACK = FALSE) **

**NULL**

其中，**x**参数输入矩阵；**symmetric**参数判断矩阵是否为对称矩阵，如果参数为空，系统将自动检测矩阵的对称性。例如：

**> A=matrix(1:9,nrow=3,ncol=3)**

**> A**

**     [,1] [,2] [,3]**

**[1,]    1    4    7**

**[2,]    2    5    8**

**[3,]    3    6    9**

**> Aeigen=eigen(A)**

**> Aeigen**

**$values**

**[1]  1.611684e+01 -1.116844e+00 -4.054214e-16**

** **

**$vectors**

**           [,1]       [,2]       [,3]**

**[1,] -0.4645473 -0.8829060  0.4082483**

**[2,] -0.5707955 -0.2395204 -0.8164966**

**[3,] -0.6770438  0.4038651  0.4082483**

得到矩阵**A**的特征值：

**> Aeigen$values**

**[1]  1.611684e+01 -1.116844e+00 -4.054214e-16**

得到矩阵A的特征向量：

**> Aeigen$vectors**

**           [,1]       [,2]       [,3]**

**[1,] -0.4645473 -0.8829060  0.4082483**

**[2,] -0.5707955 -0.2395204 -0.8164966**

**[3,] -0.6770438  0.4038651  0.4082483**


# 3 矩阵高级操作




## 3.1 Choleskey分解


对于正定矩阵**A**，可以对其进行**Choleskey**分解，**A=P’P**，其中**P**为上三角矩阵，在**R**中可以用函数**chol()**。例如：

**> A=diag(3)+1**

**> A**

**     [,1] [,2] [,3]**

**[1,]    2    1    1**

**[2,]    1    2    1**

**[3,]    1    1    2**

**> chol(A)**

**         [,1]      [,2]      [,3]**

**[1,] 1.414214 0.7071068 0.7071068**

**[2,] 0.000000 1.2247449 0.4082483**

**[3,] 0.000000 0.0000000 1.1547005**

验证**A=P’P****：**

**> t(chol(A))%*%chol(A)**

**     [,1] [,2] [,3]**

**[1,]    2    1    1**

**[2,]    1    2    1**

**[3,]    1    1    2**

也可以用**crossprod()**函数**：******

**> crossprod(chol(A),chol(A))**

**     [,1] [,2] [,3]**

**[1,]    2    1    1**

**[2,]    1    2    1**

**[3,]    1    1    2**

可以用**Choleskey**分解来计算矩阵的行列式：****

**> prod(diag(chol(A))^2)**

**[1] 4**

**> det(A)**

**[1] 4**

也可以用**Choleskey**分解来计算矩阵的逆，这时候可以用到函数**chol2inv():**

**> chol2inv(chol(A))**

**      [,1]  [,2]  [,3]**

**[1,]  0.75 -0.25 -0.25**

**[2,] -0.25  0.75 -0.25**

**[3,] -0.25 -0.25  0.75**

**> solve(A)**

**      [,1]  [,2]  [,3]**

**[1,]  0.75 -0.25 -0.25**

**[2,] -0.25  0.75 -0.25**

**[3,] -0.25 -0.25  0.75**

3.2奇异值分解

**A**为**m****×n**矩阵，矩阵的秩为**r**。**A**可以分解为**A=UDV’**，其中**U’U=V’V=I**。在**R**中可以用函数**svd()**。例如：

**> A=matrix(1:18,3,6)**

**> A**

**     [,1] [,2] [,3] [,4] [,5] [,6]**

**[1,]    1    4    7   10   13   16**

**[2,]    2    5    8   11   14   17**

**[3,]    3    6    9   12   15   18**

**> svd(A)**

**$d**

**[1] 4.589453e+01 1.640705e+00 2.294505e-15**

** **

**$u**

**           [,1]        [,2]       [,3]**

**[1,] -0.5290354  0.74394551  0.4082483**

**[2,] -0.5760715  0.03840487 -0.8164966**

**[3,] -0.6231077 -0.66713577  0.4082483**

** **

**$v**

**            [,1]       [,2]        [,3]**

**[1,] -0.07736219 -0.7196003 -0.67039144**

**[2,] -0.19033085 -0.5089325  0.55766549**

**[3,] -0.30329950 -0.2982646  0.28189237**

**[4,] -0.41626816 -0.0875968  0.07320847**

**[5,] -0.52923682  0.1230711  0.12920119**

**[6,] -0.64220548  0.3337389 -0.37157608**

**> A.u%*%diag(A.d)%*%t(A.v)**

**     ****[,1] [,2] [,3] [,4] [,5] [,6]**

**[1,]    1    4    7   10   13   16**

**[2,]    2    5    8   11   14   17**

**[3,]    3    6    9   12   15   18**


## 3.3 QR分解


**A**为**m****×****n**矩阵可以进行**QR**分解:**A=QR**，其中**Q’Q=I**，在**R**中可以用函数**qr()**来完成这个过程，例如：

**> A=matrix(1:12,4,3)**

**> qr(A)**

**$qr**

**           [,1]        [,2]          [,3]**

**[1,] -5.4772256 -12.7801930 -2.008316e+01**

**[2,]  0.3651484  -3.2659863 -6.531973e+00**

**[3,]  0.5477226  -0.3781696  7.880925e-16**

**[4,]  0.7302967  -0.9124744  9.277920e-01**

** **

**$rank**

**[1] 2**

** **

**$qraux**

**[1] 1.182574 1.156135 1.373098**

** **

**$pivot**

**[1] 1 2 3**

** **

**attr(,"class")**

**[1] "qr"**

**Rank**返回的是矩阵的秩。**Qr**项包含了**Q**矩阵和**R**矩阵的信息。要想得到**Q**矩阵和**R**矩阵，可以用**qr.Q()**函数和**qr.R()**函数：

**> qr.Q(qr(A))**

**           [,1]          [,2]       [,3]**

**[1,] -0.1825742 -8.164966e-01 -0.4000874**

**[2,] -0.3651484 -4.082483e-01  0.2546329**

**[3,] -0.5477226  4.938541e-17  0.6909965**

**[4,] -0.7302967  4.082483e-01 -0.5455419**

**> qr.R(qr(A))**

**          [,1]       [,2]          [,3]**

**[1,] -5.477226 -12.780193 -2.008316e+01**

**[2,]  0.000000  -3.265986 -6.531973e+00**

**[3,]  0.000000   0.000000  7.880925e-16**


# 4 解方程组




## 4.1普通方程组


解普通方程组可以用函数**solve()**，**solve()**的基本用法是**solve(A,b)**，其中，**A**为方程组的系数矩阵，**b**为方程组的右端。例如：

已知方程组：

**2x1+2x3=1**

**2x1+x2+2x­3=2**

**2x1+x­2=3**

解法如下：

**> A**

**     [,1] [,2] [,3]**

**[1,]    2    0    2**

**[2,]    2    1    2**

**[3,]    2    1    0**

**> b=1:3**

**>b**

**[1] 1 2 3**

**> solve(A,b)**

**[1]  1.0  1.0 -0.5**

即x­1=1，x2=1，x3=-0.5。


## 4.2 特殊方程组


对于系数矩阵是上三角矩阵和下三角矩阵的方程组。**R**中提供了**backsolve()**和**fowardsolve()**来解决这个问题。

**backsolve(r, x, k=ncol(r), upper.tri=TRUE, transpose=FALSE)**

**forwardsolve(l, x, k=ncol(l), upper.tri=FALSE, transpose=FALSE)**

这两个函数都是符合操作的函数，大致可以分为三个步骤：

①通过将系数矩阵的上三角或者下三角变为0的到新的系数矩阵,这通过upper.tri参数来实现，若upper.tri=TRUR,上三角不为0。

②通过将对步骤1中得到的新系数矩阵进行转置得到新的系数矩阵，这通过transpose参数实现，若transpose=FALSE，则步骤1中得到的系数矩阵将被转置。

③根据步骤2得到的系数矩阵来解方程组。

**X1+4X2+7X3=1**

**2X1+5X2+8X3=2**

**3X1+6X2+9X3=3**

方程组的系数矩阵为：

**> A**

**     [,1] [,2] [,3]**

**[1,]    1    4    7**

**[2,]    2    5    8**

**[3,]    3    6    9**

**> b**

**[1] 1 2 3**

**> backsolve(A,b,upper.tri=T,transpose=F)**

**[1] -0.8000000 -0.1333333  0.3333333**

过程分解：

①upper.tri=T，说明系数矩阵的上三角不为0。

**> B=A**

**> B[lower.tri(B)]=0**

**> B**

**     [,1] [,2] [,3]**

**[1,]    1    4    7**

**[2,]    0    5    8**

**[3,]    0    0    9**

②transpose=F说明系数矩阵未被转置。

③解方程：

**> solve(B,b)**

**[1] -0.8000000 -0.1333333  0.3333333**


# 5 其它




## 5.1矩阵的向量化


将矩阵向量化有时候是必要的。矩阵的向量化可以通过**as.vector()**来实现：

**> A**

**     [,1] [,2] [,3] [,4]**

**[1,]    1    4    7   10**

**[2,]    2    5    8   11**

**[3,]    3    6    9   12**

将矩阵元素向量化：

**> as.vector(A)**

** [1]  1  2  3  4  5  6  7  8  9 10 11 12**

将矩阵的方阵部分元素向量化：

**> as.vector(A[1:min(dim(A)),1:min(dim(A))])**

**[1] 1 2 3 4 5 6 7 8 9**


## 5.2矩阵的合并




### 5.2.1矩阵的列合并


矩阵的列合并可以通过**cbind()**来实现。

**> A**

**     [,1] [,2] [,3]**

**[1,]    1    4    7**

**[2,]    2    5    8**

**[3,]    3    6    9**

**> B=1:3**

**> cbind(A,B)**

**           B**

**[1,] 1 4 7 1**

**[2,] 2 5 8 2**

**[3,] 3 6 9 3**


### 5.2.2矩阵的行合并


矩阵的行合并可以通过**rbind()**来实现。

**> A**

**     [,1] [,2] [,3]**

**[1,]    1    4    7**

**[2,]    2    5    8**

**[3,]    3    6    9**

**> B=1:3**

**> rbind(A,B)**

**  [,1] [,2] [,3]**

**     1    4    7**

**     2    5    8**

**     3    6    9**

**B    1    2    3**


## 5.3 时序矩阵的滞后


在时间序列中经常会用到一个序列的滞后序列，**R**中的包**fMultivar**中的函数**tslag()**提供了这个功能。

**> library(fMultivar)**

**Loading required package: sn**

**Loading required package: mnormt**

**Package 'sn', 0.4-16 (2010-08-30). Type 'help(SN)' for summary information**

**Loading required package: timeDate**

**Loading required package: timeSeries**

**Loading required package: fBasics**

**Loading required package: MASS**

** **

**Attaching package: 'fBasics'**

** **

**The following object(s) are masked from 'package:base':**

** **

**    norm**

**> args(tslag)**

**function (x, k = 1, trim = FALSE) **

**NULL**

其中：x为一个向量，k指定滞后阶数，可以是一个自然数列，若trim为假，则返回序列与原序列长度相同，但含有NA值；若trim项为真，则返回序列中不含有NA值，例如：

**> x=1:9**

**> x**

**[1] 1 2 3 4 5 6 7 8 9**

**> tslag(x,1:4,trim=F)**

**      [,1] [,2] [,3] [,4]**

** [1,]   NA   NA   NA   NA**

** [2,]    1   NA   NA   NA**

** [3,]    2    1   NA   NA**

** [4,]    3    2    1   NA**

** [5,]    4    3    2    1**

** [6,]    5    4    3    2**

** [7,]    6    5    4    3**

** [8,]    7    6    5    4**

** [9,]    8    7    6    5**

**> tslag(x,1:4,trim=T)**

**     [,1] [,2] [,3] [,4]**

**[1,]    4    3    2    1**

**[2,]    5    4    3    2**

**[3,]    6    5    4    3**

**[4,]    7    6    5    4**

**[5,]    8    7    6    5**
