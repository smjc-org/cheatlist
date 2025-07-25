# 杂项

## 逃离黑洞

```sas
 ;*';*";*/;run;quit;
```

## 在单引号内解析宏变量

```sas
%unquote(%str(%')%superq(macro_variable)%str(%'))
```

> [!NOTE]
>
> `%superq()` 确保宏变量只会解析一层，若解析后的值包含 `%`, `&`，不会继续解析。

## 规避 `WARNING: 指定的查询涉及按 SELECT 子句中没出现的一项排序。由于您正排序 SELECT DISTINCT 的输出，可能出现部分重复项未删除的情况。` 问题

将下面的代码：

```sas
proc sql noprint;
    create table out as
        select
            distinct usubjid
        from adsl
        order by armn;
quit;
```

改为：

```sas
proc sql noprint;
    create table out(drop = armn) as
        select
            a.usubjid,
            b.armn
        from (select distinct usubjid from adsl) as a left join adsl as b on a.usubjid = b.usubjid
        order by b.armn;
quit;
```

## 克隆文件夹结构（不复制文件）

```bash
robocopy "源文件夹路径" "目标文件夹路径" /e /xf *
```

- `/e`: 复制所有子目录，包括空目录
- `/s`: 复制所有子目录，但不包括空目录
- `/xf *`: 排除所有文件，即不复制任何文件
