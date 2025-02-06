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
