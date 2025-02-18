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
