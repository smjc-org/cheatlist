# ADaM 编程参考

## 复制数据集

```sas
proc datasets noprint nowarn;
    copy in = rawdata out = work;
    select ae;
    copy in = adam out = work;
    select adsl;
run;
quit;
```

## 清除格式

```sas
proc datasets library = work noprint nowarn;
    modify ae;   attrib _all_ format= informat=;
    modify adsl; attrib _all_ format= informat=;
run;
quit;
```

## 重新排序

```sas
proc sort data = ae;
    by subjid aestdat aeterm;
run;
data ae;
    set ae
    by subjid aestdat aeterm;

    retain aeseq;

    if first.subjid then aeseq = 1;
    else aeseq + 1;
run
```

## BDS 衍生基础框架

### 简单情况

```sas
proc format;
    value paramn
        1 = "体温（℃）"
        2 = "心率（次/分）"
        3 = "呼吸（次/分）"
        4 = "收缩压（mmHg）"
        5 = "舒张压（mmHg）"
        6 = "体重（Kg）";

    value AVISITN
        1 = "筛选期V1"
        2 = "治疗期V2"
        3 = "治疗期V3"
        4 = "随访期V4"
        5 = "随访期V5"
        6 = "随访期V6";
run;

data dummy;
    set adsl;

    length PARAM $40 PARAMN 8 AVISIT $40 AVISITN 8;

    do PARAMN = 1 to 6;
        PARAM = put(PARAMN, PARAMN.);
        do AVISITN = 1 to 6;
            AVISIT = put(AVISITN, AVISITN.);
            output;
        end;
    end;
run;
```

### 复杂情况

```sas
proc format;
    value PARCAT1N
        1 = "实验室检查-血常规"
        2 = "实验室检查-血生化"
        3 = "实验室检查-凝血常规"
        4 = "实验室检查-尿常规"
        5 = "实验室检查-妊娠试验"
        6 = "实验室检查-传染病";
    value PARAMN
        1 = "白细胞计数（10^9/L）"
        2 = "红细胞计数（10^12/L）"
        3 = "血红蛋白含量（g/L）"
        4 = "血小板计数（10^9/L）"
        5 = "中性粒细胞计数（10^9/L）"
        6 = "中性粒细胞比值（%）"

        7 = "谷丙转氨酶（IU/L）"
        8 = "谷草转氨酶（IU/L）"
        9 = "血清白蛋白（g/L）"
        10 = "血清总胆红素（umol/L）"
        11 = "血清肌酐（umol/L）"
        12 = "尿素（mmol/L）"
        13 = "尿素氮（mmol/L）"

        14 = "凝血酶原时间（s）"
        15 = "活化部分凝血活酶时间（s）"
        16 = "国际标准化比值"

        17 = "尿糖"
        18 = "尿蛋白"
        19 = "尿红细胞计数"
        20 = "尿白细胞计数"

        21 = "妊娠试验"

        22 = "乙型肝炎表面抗原"
        23 = "乙肝e抗原"
        24 = "乙肝核心抗体"
        25 = "丙型肝炎抗体"
        26 = "HIV抗体"
        27 = "梅毒抗体";
    value AVISITN
        1 = "筛选期V1"
        2 = "治疗期V2"
        3 = "治疗期V3"
        4 = "随访期V4"
        5 = "随访期V5"
        6 = "随访期V6";
run;

data dummy;
    set adsl;

    length PARCAT1 $40 PARCAT1N 8 PARAM $40 PARAMN 8 AVISIT $40 AVISITN 8;

    do PARCAT1N = 1 to 6;
        PARCAT1 = put(PARCAT1N, PARCAT1N.);
        select (PARCAT1N);
            when (1)
                do PARAMN = 1 to 6;
                    PARAM = put(PARAMN, PARAMN.);
                    do AVISITN = 1, 4 to 6;
                        AVISIT = put(AVISITN, AVISITN.);
                        output;
                    end;
                end;
            when (2)
                do PARAMN = 7 to 13;
                    PARAM = put(PARAMN, PARAMN.);
                    do AVISITN = 1, 4 to 6;
                        AVISIT = put(AVISITN, AVISITN.);
                        output;
                    end;
                end;
            when (3)
                do PARAMN = 14 to 16;
                    PARAM = put(PARAMN, PARAMN.);
                    do AVISITN = 1, 4 to 6;
                        AVISIT = put(AVISITN, AVISITN.);
                        output;
                    end;
                end;
            when (4)
                do PARAMN = 17 to 20;
                    PARAM = put(PARAMN, PARAMN.);
                    do AVISITN = 1, 4 to 6;
                        AVISIT = put(AVISITN, AVISITN.);
                        output;
                    end;
                end;
            when (5)
                do PARAMN = 21 to 21;
                    PARAM = put(PARAMN, PARAMN.);
                    do AVISITN = 1, 4 to 6;
                        AVISIT = put(AVISITN, AVISITN.);
                        output;
                    end;
                end;
            when (6)
                do PARAMN = 22 to 27;
                    PARAM = put(PARAMN, PARAMN.);
                    do AVISITN = 1, 4 to 6;
                        AVISIT = put(AVISITN, AVISITN.);
                        output;
                    end;
                end;
        end;
    end;
run;
```

## 比较差异

```sas
ods html5 path = "&PATH_STAT\04 ADS程序\02 QC程序\log" file = "v-adae.html";
    proc compare base = adam.adae compare = qc_adae listall;
        id usubjid aeseq;
    run;
ods html5 close;
```
