extract(year from p_orderdate) = 1995
like ' '用单引号
AND c1.c_custkey < c2.c_custkey 去重
group by 要在having之后
查询 1996 年 7 月的销售冠军，即该月销售额最高的供应商。
SELECT l_suppkey,
       SUM(l_extendedprice * (1 - l_discount)) AS sales_amount
FROM lineitem
WHERE l_shipdate >= DATE '1996-07-01'
  AND l_shipdate <  DATE '1996-08-01'
GROUP BY l_suppkey
ORDER BY sales_amount DESC；