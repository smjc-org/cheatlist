# 常用输出格式

## 数值变量

```sas
proc format;
    /*率*/
    picture srate(round)
            low - < -1 = '#ERROR'(noedit)
            -1         = '-100.0'(noedit)
            -1 < - < 0 = '-09.9'(multiplier = 1000 prefix = '-')
            0 - < 1    = '09.9'(multiplier = 1000)
            1          = '100.0'(noedit)
            1 < - high = '#ERROR'(noedit);
    /*检验统计量*/
    picture sstat(round)
            0          = '0.0000'(noedit)
            0 < - high = '09.9999'
            low - < 0  = '009.9999'(prefix = '-');
    /*P值*/
    picture spvalue(round  max = 6)
        low - < 0.0001 = '<0.0001'(noedit)
        other          = '9.9999';
run;
```

## 字符变量

### 是否

```sas
proc format;
    value y1n
        1 = "是"
        2 = "否";
quit;
```

### 有无

```sas
proc format;
    value y2n
        1 = "有"
        2 = "无";
quit;
```

### 组别

```sas
proc format;
    value armn
        1 = "试验组"
        2 = "对照组";
quit;
```

### 访视

```sas
proc format;
    value avisitn
        1 = "筛选期V1"
        2 = "治疗期V2"
        3 = "治疗期V3"
        4 = "随访期V4"
        5 = "随访期V5"
        6 = "随访期V6";
quit;
```

### 性别

```sas
proc format;
    value sexn
        1 = "男"
        2 = "女";
quit;
```

### 临床意义评价

```sas
proc format;
    value clsign
        1 = "正常"
        2 = "异常无临床意义"
        3 = "异常有临床意义";
quit;
```

### 方案偏离严重程度

```sas
proc format;
    value dvsevn
        1 = "轻度"
        2 = "严重";
quit;
```

### 不良事件严重程度

```sas
proc format;
    value aesevn
        1 = "1级"
        2 = "2级"
        3 = "3级"
        4 = "4级"
        5 = "5级";
quit;
```

### 易用性评估

```sas
proc format;
    value evaresn
        1 = "1级：很差"
        2 = "2级：差"
        3 = "3级：一般"
        4 = "4级：好"
        5 = "5级：非常好";
quit;
```
