---
title: LN
---

返回 `x` 的自然对数，即以 e 为底的 `x` 的对数。如果 `x` 小于或等于 0.0E0，则函数返回 NULL。

## 语法

```sql
LN( <x> )
```

## 示例

```sql
SELECT LN(2);

┌────────────────────┐
│        ln(2)       │
├────────────────────┤
│ 0.6931471805599453 │
└────────────────────┘
```