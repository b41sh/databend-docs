---
title: BITMAP_NOT
---

生成一个新的位图，其中包含第一个位图中不在第二个位图中的元素。

## 语法

```sql
BITMAP_NOT( <bitmap1>, <bitmap2> )
```

## 别名

- [BITMAP_AND_NOT](bitmap-and-not.md)

## 示例

```sql
SELECT BITMAP_NOT(BUILD_BITMAP([1,4,5]), BUILD_BITMAP([5,6,7]))::String;

┌──────────────────────────────────────────────────────────────────────┐
│ bitmap_not(build_bitmap([1, 4, 5]), build_bitmap([5, 6, 7]))::string │
├──────────────────────────────────────────────────────────────────────┤
│ 1,4                                                                  │
└──────────────────────────────────────────────────────────────────────┘

SELECT BITMAP_AND_NOT(BUILD_BITMAP([1,4,5]), BUILD_BITMAP([5,6,7]))::String;

┌──────────────────────────────────────────────────────────────────────────┐
│ bitmap_and_not(build_bitmap([1, 4, 5]), build_bitmap([5, 6, 7]))::string │
├──────────────────────────────────────────────────────────────────────────┤
│ 1,4                                                                      │
└──────────────────────────────────────────────────────────────────────────┘
```