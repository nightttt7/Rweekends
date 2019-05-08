# 控制流
```
# for
for(i in 1:3){
    print(i)
}

# while
i <- 1
while(i <= 3){
    print(i)
    i <- i+1
}

# if...else if...else
x <- 0.1
if(x < -1){
    print(-1)
} else if(x > 1){
    print(1)
} else {
    print(0)
}

# ifelse
ifelse(x>0,"positive","notpositive")

# switch
switch("2",
    "1" = "hello",
    "2" = "hi"
    )
```

# 函数
```
my <- function(name){
    re <- paste("hello",name)
    return(re)
}
my("test")
```

# 常用函数

### 数学
```
# random uniform
runif(2)
# random normal
rnorm(2)
# 求余
10%%3
# 整除
10%/%3
abs(-2)
sqrt(2)
ceiling(2.2)
floor(2.2)
# 取整数部分
trunc(-2.22222)
# 四舍五入到指定位的小数
round(3.14,1)
# 四舍五入到指定的有效数字位数
signif(3.14,1)
log(2.718282)
log(8,base=2)
log10(100)
exp(1)
x=c(1,1,1,1,1,2,2,5,6,7,7)
sum(x)
length(x)
mean(x)
median(x)
sd(x)
var(x)
# 绝对中位差
mad(x)
min(x)
max(x)
range(x)
quantile(x,c(.25,.5,.75))
# Tukey's five-number summary
summary(x)
fivenum(x)
# 滞后差分
diff(x,lag=2)
# 标准正态化
scale(x)
# 严格等于,浮点数慎用
3 == 3
3 != 3
# 或
3>2 | 4<= 5
# 与
2 ^ 3 == 8 & 2 ** 3 ==8
```

### 日期
```
# today
Sys.Date()
# 读取字符串日期为date
t <- as.Date("09/22/2019","%m/%d/%y")
# 从日期中获取特定值
format(t, format="%B,%d,%A")
# 日期计算
difftime(t, as.Date("1989-06-04"), units="weeks")
```

### 重构 reshape
```
library(reshape2)
# 短数据格式,变量作为列名(索引除外)),有多列
mydata <- read.table(header=TRUE, sep=" ", text="
id time X1 X2
1 1 5 6
1 2 3 5
2 1 6 1
2 2 2 4
")
# 重构为长数据格式,变量一列,值一列(索引除外),索引由id指定
mydata <- melt(mydata, id=(c("id","time")))
# 重构为短数据格式,左为索引,右为列名(字符串可以拼接)
## dcast: to data.frame
dcast(mydata,id+time~variable)
dcast(mydata,id~variable+time)
## acast: to vector/matrix/array
acast(mydata,id+time~variable)
acast(mydata,id~variable+time)
```
