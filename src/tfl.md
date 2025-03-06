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

## Listing 输出 RTF 使用 `order` 变量

```sas
column usubjid erlid dvseq dvterm dvstdtc dvreas dvsev dvacn dvres;
define usubjid / order order = data "筛选号";
define erlid   / order order = data "入组号";
define dvseq   / "序号";
define dvterm  / "偏离描述";
define dvstdtc / "发生日期";
define dvreas  / "发生原因";
define dvsev   / "严重程度";
define dvacn   / "纠正/预防措施";
define dvres   / "结果";
```

## @S 行内格式化

```sas
column ("@S={just=l}AE类型" item)
       ("@S={borderbottomcolor=black borderbottomwidth=0.5pt}合计 N=&n" value times_fmt);
```

## RTF 首列左对齐

```sas
define item  / display "    严重程度"
               style(header) = {protectspecialchars=off just=l}
               style(column) = {protectspecialchars=off just=l};
```
