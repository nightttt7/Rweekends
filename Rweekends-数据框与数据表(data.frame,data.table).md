# 数据框 data.frame
- 做统计,金融等最常用的数据结构
- 个人更建议使用data.table,两者可以很方便互相转化
- data.table拥有更加便捷的操作方式,但是data.frame的兼容性更好.

```
id <- c(1,2,3,4)
age <- c(25,34,28,52)
diabetes <- c("type1", "type2", "type1", "type2")
status <- c("poor","improved","excellent","poor")
patientdata <- data.frame(id,age,diabetes,status)
# 选取行
patientdata[,1]
patientdata[,1:2]
patientdata[,c(1,3)]
# 选取列
patientdata[1]
patientdata[1:2]
patientdata[c(1,3)]
patientdata["age"]
patientdata[c("age","status")]
patientdata$status
table(patientdata$status,patientdata$age)
# 选取值
patientdata[1,2]
patientdata[1:2,1:2]
patientdata[c(1,3),c(1,3)]
# 转换成数据框
# as.data.frame(d)
```

# 数据表 data.table
- 在我用过的各个语言的类数据框数据结构中中,data.table是操作最便捷的,代码量最少的
- a high-performance version of base R's data.frame with syntax and feature enhancements for ease of use, convenience and programming speed

### base
```
library(data.table)

# create a data.table
# dt is a 12 rows, 4 cols data.table
dt <- data.table(V1=c(1,2), V2=LETTERS[1:3], V3=round(rnorm(4),2), V4=1:12)

# by rows
dt[3:5]
dt[3:5,]
dt[V2 == "A"]
dt[V2 %in% c("A","C")]

# by cols
dt[,.(V2)]
dt[,.(V2,V3)]
dt[,sum(V1)]
dt[,.(sum(V1),sd(V3))]
dt[,.(Aggregate = sum(V1), Sd.V3 = sd(V3))]
dt[,.(V1, Sd.V3 = sd(V3))]

# use by
dt[,.(V4.Sum = sum(V4)),by=V1]
dt[,.(V4.Sum = sum(V4)),by=.(V1,V2)]
dt[,.(V4.Sum = sum(V4)),by=sign(V1-1)]
dt[1:5,.(V4.Sum = sum(V4)),by=V1]
dt[,.N,by=V1]

# add & delete
## use [] to show the result
dt[, V1 := round(exp(V1),2)][]
dt[, c("V1","V2") := list(round(exp(V1),2), rep(LETTERS[4:6],4))]
dt[, ':=' (V1 = V1/5 , V2 = rep(LETTERS[7:9],4))]
DT[, V1 := NULL]
DT[, c("V1","V2") := NULL]
Cols.chosen = c("V1","V2")
DT[, (Cols.chosen) := NULL]
```

### 主键 key
```
dt <- data.table(V1=c(1,2), V2=LETTERS[1:3], V3=round(rnorm(4),2), V4=1:12, key = "V2")
setkey(dt,V2)
key(dt)
haskey(dt)
dt["A"]
dt[c("A","C")]
# only the first one
DT["A", mult ="first"]
# only the last one
DT["A", mult = "last"]
# not show the nomatch terms
DT[c("A","D"), nomatch = 0]
DT[c("A","C"), sum(V4), by=.EACHI]
setkey(dt,V1,V2)
dt[.(2,"C")]
```

### others
```
# .SD
dt<- data.table(V1=c(1L,2L), V2=LETTERS[1:3],
                V3=round(rnorm(4),4), V4=1:12)
dt[, print(.SD), by=V2]
dt[,.SD[c(1,.N)], by=V2]
dt[, lapply(.SD, sum), by=V2]
# set
setnames(DT,c("V2","V3"),c("V2.rating","V3.DataCamp"))
setcolorder(DT,c("V2","V1","V4","V3"))
# convert existing objects
## for data.frames and lists
setDT(df) 
## for other structures
as.data.table(mt) 
```
