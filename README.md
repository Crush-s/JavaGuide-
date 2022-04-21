# JavaGuide-

# Oracle
## 函数
### null判断并替换空值
1.NVL()

从两个表达式返回一个非 null 值。
语法
NVL(eExpression1, eExpression2)
参数
eExpression1, eExpression2

如果 eExpression1 的计算结果为 null 值，则 NVL( ) 返回 eExpression2。如果 eExpression1 的计算结果不是 null 值，则返回 eExpression1。eExpression1 和 eExpression2 可以是任意一种数据类型。如果 eExpression1 与 eExpression2 的结果皆为 null 值，则 NVL( ) 返回 .NULL.。

返回值类型

字符型、日期型、日期时间型、数值型、货币型、逻辑型或 null 值

2.NULLIF()

如果两个指定的表达式相等，则返回空值。
语法NULLIF ( expression1 , expression2 )
参数expression1, expression2
常量、列名、函数、子查询或算术运算符、按位运算符以及字符串运算符的任意组合。
返回类型与第一个 expression1 相同。

NULLIF与DECODE

NULLIF(param,0)等效于DECODE（param，0，null,param)：如果param为0，则返回null，否则返回param。

3.COALESCE()

Oracle COALESCE函数语法为COALESCE(表达式1,表达式2,...,表达式n)，n>=2,此表达式的功能为返回第一个不为空的表达式，如果都为空则返回空值。

注意：所有表达式必须为同一类型或者能转换成同一类型。

4.DECODE()

decode(条件,值1,返回值1,值2,返回值2,...值n,返回值n,缺省值)

该函数的含义如下：

IF 条件=值1 THEN
　　　　RETURN(返回值1)
ELSIF 条件=值2 THEN
　　　　RETURN(返回值2)
　　　　......
ELSIF 条件=值n THEN
　　　　RETURN(返回值n)
ELSE
　　　　RETURN(缺省值)
END IF
