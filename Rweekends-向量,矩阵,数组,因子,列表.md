# 向量 vector
- 向量是R语言最基本的基本数据结构,'numeric'或者'character'等,都是不同类型的向量.
- 不可否认的是,这个特性会带来很多麻烦.

### 创建,输出
```
a <- c(1,2,3,4,5)
a <- 1:5
a <- seq(1,5,1)
a[c(1,2)]
a[c(2:4)]
```

# 矩阵 matrix
- R语言的矩阵可用于线性代数运算,被几乎所有的package支持
- 除了矩阵,R语言还拥有data.frame,data.table等复杂数据结构

### 创建,输出
```
# 按行计数
matrix(1:12,3,4,byrow=TRUE)
# 按列计数(默认)
matrix(1:12,3,4,byrow=FALSE)
# 分步进行
x <- 1:12
dim(x) <- c(3,4)
x
# 单位对角矩阵,对角矩阵,零矩阵,单位矩阵
diag(3)
diag(c(1,2,3))
diag(diag(c(1,2,3)))
matrix(0,2,2)
matrix(1,2,2)

# with row/col names
rnames <- c('r1','r2')
cnames <- c('c1','c2')
cells <- c(11,12,21,22)
mymatrix <- matrix(cells, nrow=2, ncol=2, byrow=TRUE, dimnames=list(rnames,cnames))
# change row/col names
colnames(mymatrix) <- c("cname1","cname2")
# 横向拼接
cbind(c(1,2,3),c(4,5,6))
# 纵向拼接
rbind(c(1,2,3),c(4,5,6))
# 输出矩阵
mymatrix <- matrix(1:9,3,3)
mymatrix[,3]
mymatrix[3,]
## 如果不加逗号, 将输出矩阵整体的第x个元素
mymatrix[3]
mymatrix[2,2]
mymatrix[1:2,c(1,2)]
## 负号表示这些除外
mymatrix[-1,]
```

### 矩阵运算
```
a <- matrix(1:6,2,3)
nrow(a)
ncol(a)
t(a)
rowSums(a)
rowMeans(a)
b <- matrix(7:12,3,2)
# inner
a %*% b
# outer
a %o% b
kronecker(a,b)
s = matrix(rnorm(9),nrow=3,ncol=3)
det(s)
# solve multi
solve(s,c(1,2,3))
# inverse
solve(s)
# check inverse
round(s%*%solve(s))
# eigen value an vector
eigen(s)
eigen(s)$values
eigen(s)$vector
# change matrix to vector
as.vector(s)
```

# 数组 array
- 高维矩阵
```
dim1 <- c("a1","a2")
dim2 <- c("b1","b2","b3")
dim3 <- c("c1","c2","c3","c4")
print(array(1:24,c(2,3,4),dimnames=list(dim1, dim2, dim3)))
```
# 因子 factor

### 无序因子
```
f <- c("type1", "type2", "type1", "type2")
f <- factor(f)
```

### 有序因子
```
f <- c("poor","improved","excellent","poor")
f <- factor(f, order=TRUE, levels = c("poor","improved","excellent"))
```

### 使用
```
state <- c("tas", "sa", "qld", "nsw", "nsw", "nt", "wa", "wa", "qld", "vic", "nsw", 
"vic", "qld", "qld", "sa", "tas","sa", "nt", "wa", "vic", "qld", "nsw", "nsw", "wa",
"sa", "act", "nsw", "vic", "vic", "act")
statef <- factor(state)
incomes <- c(60, 49, 40, 61, 64, 60, 59, 54, 62, 69, 70, 42, 56, 61, 61, 61, 58, 51, 
48, 65, 49, 49, 41, 48, 52, 46, 59, 46, 58, 43)
# 均值标准差
tapply(incomes, statef, mean)
tapply(incomes, statef, sd)
# 置信区间
inv <- function (x,perc) (c(mean(x)-qnorm(perc)*sd(x), mean(x)+qnorm(perc)*sd(x)))
inctest <- tapply(incomes, statef, test, .95)

# 列表 list
```
g <- "my list"
h <- c(25,26,18,39)
j <- matrix(1:10,nrow=5)
k <- c("one","two","three")
mylist <- list(title=g, age=h, j, k)
mylist[[2]]
mylist[["age"]]
```
