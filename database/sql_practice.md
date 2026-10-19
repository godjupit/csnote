# SQL 基础练习（第一组）

根据 `sql_example.md` 的范围，使用 PostgreSQL 的 TPC-H 数据库完成下面 10 道查询题。本组只列题目，不附答案。

说明：题干在各项要求旁标注了对应的数据库字段名；“数量”“平均值”等统计结果需要通过查询计算，不是原表中已有的字段。

注意：实际品牌值是 `Brand#43` 这种形式，PostgreSQL 的 `LIKE` 区分大小写。

## 1. 模糊查询与排序

查询 `part` 表中，品牌 `p_brand` 以 `Brand#3` 开头、类型 `p_type` 包含 `BRASS` 的商品。显示商品编号 `p_partkey`、名称 `p_name`、品牌 `p_brand`、类型 `p_type` 和尺寸 `p_size`，按尺寸 `p_size` 降序、商品编号 `p_partkey` 升序排列。

## 2. 分组统计与分组筛选

查询 `customer` 表中各市场区域 `c_mktsegment` 的客户数量（统计客户编号 `c_custkey`）和平均账户余额（对 `c_acctbal` 求平均值）。显示市场区域及以上两项统计结果。只保留客户数量超过 290 的区域，按平均账户余额降序排列。

## 3. 日期筛选与前 N 条记录

查询 `orders` 表中，下单日期 `o_orderdate` 在 1995 年内且优先级 `o_orderpriority` 包含 `URGENT` 的订单。显示订单编号 `o_orderkey`、日期 `o_orderdate`、优先级 `o_orderpriority` 和总金额 `o_totalprice`，按总金额 `o_totalprice` 降序排列，只显示前 10 条。

## 4. 集合条件与算术表达式

查询 `lineitem` 表中，发货模式 `l_shipmode` 为 `AIR` 或 `TRUCK`、数量 `l_quantity` 大于 30 的明细。显示订单编号 `l_orderkey`、商品编号 `l_partkey`、数量 `l_quantity`，以及实际金额（扩展价格 `l_extendedprice` 乘以（1 减折扣 `l_discount`））：`l_extendedprice * (1 - l_discount)`，将实际金额命名为 `actual_amount`。

## 5. 按季度统计

统计 `lineitem` 表中，1995—1996 年每年各季度的发货明细数量，以发货日期 `l_shipdate` 为准。显示年份（从 `l_shipdate` 提取）、季度（从 `l_shipdate` 提取）和明细数量（统计明细行数），只保留明细数量超过 1000 的组，按年份、季度升序排列。

可使用例题涉及的 `EXTRACT` 提取年份和季度。

## 6. 三表连接

查询每个地区的供应商数量。连接 `region`、`nation`、`supplier`，显示地区名称 `r_name` 和供应商数量，按供应商数量降序排列。

连接字段：`region.r_regionkey` 与 `nation.n_regionkey` 对应，`nation.n_nationkey` 与 `supplier.s_nationkey` 对应。供应商数量通过统计供应商编号 `s_suppkey` 得到。

## 7. 连接、聚合与 HAVING

查询每个国家的客户数量和平均账户余额。连接 `nation` 和 `customer`，显示国家名称 `n_name`、客户数量（统计客户编号 `c_custkey`）及平均账户余额（对 `c_acctbal` 求平均值），只保留平均账户余额大于 4000 的国家。

连接字段：`nation.n_nationkey` 与 `customer.c_nationkey` 对应。

## 8. 存在与不存在的子查询

分别编写两条 SQL：

1. 查询至少下过一笔订单的客户，显示客户编号 `c_custkey` 和名称 `c_name`，每个客户只出现一次。
2. 查询从未下过订单的客户，显示客户编号 `c_custkey` 和名称 `c_name`。

涉及 `customer` 和 `orders` 两张表，客户编号 `customer.c_custkey` 与订单所属客户编号 `orders.o_custkey` 对应。尝试分别使用 `EXISTS` 和 `NOT EXISTS`。

## 9. 自连接与去除重复组合

在 `customer` 表中查询国家编号 `c_nationkey` 相同、且市场区域 `c_mktsegment` 不同的客户对。显示两个客户的编号 `c_custkey`、名称 `c_name` 和共同的国家编号 `c_nationkey`。要求不能将客户与自身配对，同一对客户只出现一次，例如出现 `(1, 2)` 后不能再出现 `(2, 1)`。

## 10. 相关子查询

在 `orders` 表中查询订单总金额 `o_totalprice` 高于该客户自身平均订单金额（对相同客户编号 `o_custkey` 的所有订单的 `o_totalprice` 求平均值）的订单。显示订单编号 `o_orderkey`、客户编号 `o_custkey` 和订单总金额 `o_totalprice`，按客户编号 `o_custkey` 升序、订单总金额 `o_totalprice` 降序排列。
