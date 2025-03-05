# TFL 编程

## Listing order 变量处理

```sas
data l_7_3_1;
    set l_7_3_1;
    by arm siteid usubjid rnumber aeseq notsorted;
    if not first.arm then arm = "";
    if not first.siteid then siteid = "";
    if not first.usubjid then usubjid = "";
    if not first.rnumber then rnumber = "";
run;
```

## @S 行内格式化

```sas
column ("@S={just=l}AE类型" item)
       ("@S={borderbottomcolor=black borderbottomwidth=0.5pt}合计 N=&n" value times_fmt);
```

## RTF 第一列左对齐

```sas
define item  / display "    严重程度"
               style(header) = {protectspecialchars=off just=l}
               style(column) = {protectspecialchars=off just=l};
```
