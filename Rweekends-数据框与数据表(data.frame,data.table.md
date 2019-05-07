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
- 在我用过的各个语言的类数据框数据结构中中,这是操作最便捷的,代码量最少的
```

```
