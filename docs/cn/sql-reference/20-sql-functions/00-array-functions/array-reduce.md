---
title: ARRAY_REDUCE
---

通过迭代地将 lambda 函数应用于数组元素，将数组缩减为单个值。

## 语法

```sql
ARRAY_REDUCE( <array>, <lambda> )
```

## 示例

```sql
SELECT ARRAY_REDUCE([1, 2, 3, 4], (x,y) -> x + y);

┌───────────────────────────────────────────────┐
│ array_reduce([1, 2, 3, 4], (x, y) -> (x + y)) │
├───────────────────────────────────────────────┤
│                                            10 │
└───────────────────────────────────────────────┘
```
