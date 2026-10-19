extract(year from p_orderdate) = 1995
like ' '用单引号
AND c1.c_custkey < c2.c_custkey 去重
group by 要在having之后