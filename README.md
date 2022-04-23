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

`decode(条件,值1,返回值1,值2,返回值2,...值n,返回值n,缺省值)`

该函数的含义如下：

`IF 条件=值1 THEN
　　　　RETURN(返回值1)
ELSIF 条件=值2 THEN
　　　　RETURN(返回值2)
　　　　......
ELSIF 条件=值n THEN
　　　　RETURN(返回值n)
ELSE
　　　　RETURN(缺省值)
END IF`
### 日期型函数
1.**为日期加上指定月份函数**

ADD_MONTHS(date,integer)函数。该函数将返回在指定的日期上加一个月份数后的日期。各参数具体含义如下：

❑date：指定的日期。

❑integer：要加的月份数，该值如果为负数，则表示减去的月份数。

sysdate - 1/6、sysdate - 1/24/60表示什么：
1.如果是A/B类型，则表示往前推n小时，A表示天数，B表示小时，n = A×24/B。

例如：sysdate - 1/6，此处A = 1；B = 6。

n = 1×24/6 = 4

即 select sysdate - 1/6 from dual 得出的时间是当前时间往前推4小时

2.如果是A/B/C类型。则表示往前推m分钟，A表示天数，B表示小时，C表示分钟。

m的算法： 先计算 A×24/B 得到需要往前推多少小时，假设n = A×24/B。

那么 m = n×60/C。（1小时=60分钟，所以n小时要乘以60，再去除以C，得到往前推的分钟数）

即 select sysdate - 1/24/60 from dual 得出的时间是当前时间往前推1分钟

例子：

1.1获取指定时间段内的日期列表

获取2021-09-22至2021-10-03时间段内的所有日期

`SELECT TO_CHAR(TO_DATE('2021-09-22', 'yyyy-MM-dd') + ROWNUM - 1, 'yyyyMMdd') as datelist
  FROM DUAL
CONNECT BY ROWNUM <=
           trunc(to_date('2021-10-03', 'yyyy-MM-dd') -
                 to_date('2021-09-22', 'yyyy-MM-dd')) + 1`

1.2获取指定时间段内的月份列表

获取2021-09至2022-06时间段的所有月份

`SELECT TO_CHAR(ADD_MONTHS(TO_DATE('2021-09', 'yyyy-MM'), ROWNUM - 1),
               'yyyyMM') as monthlist
  FROM DUAL
CONNECT BY ROWNUM <=
           months_between(to_date('2022-06', 'yyyy-MM'),
                          to_date('2021-09', 'yyyy-MM')) + 1 `

1.3获取指定时间段内的年份列表

获取2021-09至2023-11时间段的所有年份

`SELECT TO_CHAR(ADD_MONTHS(TO_DATE('2021-09', 'yyyy-MM'), (ROWNUM - 1) * 12),
               'yyyy') as yearlist
  FROM DUAL
CONNECT BY ROWNUM <=
           months_between(to_date('2023-11', 'yyyy-MM'),
                          to_date('2021-09', 'yyyy-MM')) / 12 + 1`

2.**返回当前会话的时区**

`SELECT SESSIONTIMEZONE FROM DUAL;`

