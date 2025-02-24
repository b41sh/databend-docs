---
title: CREATE VIRTUAL COLUMN
sidebar_position: 1
---

import FunctionDescription from '@site/src/components/FunctionDescription';

<FunctionDescription description="引入或更新版本：v1.2.339"/>

import EEFeature from '@site/src/components/EEFeature';

<EEFeature featureName='VIRTUAL COLUMN'/>

为表创建虚拟列。请注意，虚拟列仅支持 [FUSE Engine](../../../00-sql-reference/30-table-engines/00-fuse.md)，并且专为与 [Variant](../../../00-sql-reference/10-data-types/variant.md) 数据类型兼容而设计。有关列定义，请参阅 [访问 JSON 中的元素](../../../00-sql-reference/10-data-types/variant.md#accessing-elements-in-json)。

请注意，在为已包含 Variant 数据的表创建虚拟列后，需要使用 [REFRESH VIRTUAL COLUMN](refresh-virtual-column.md) 命令刷新虚拟列。

## 语法

```sql
CREATE [ OR REPLACE ] VIRTUAL COLUMN [ IF NOT EXISTS ] ( <virtual_column_1>, <virtual_column_2>, ... ) FOR <table>
```

## 示例

以下示例为名为 'test' 的表创建虚拟列：

```sql
-- 创建一个名为 'test' 的表，包含 'id' 和 'val' 列，类型为 Variant。
CREATE TABLE test(id int, val variant);

-- 向 'test' 表中插入一条包含 Variant 数据的示例记录。
INSERT INTO
  test
VALUES
  (
    1,
    '{"id":1,"name":"databend","tags":["powerful","fast"],"pricings":[{"type":"Standard","price":"Pay as you go"},{"type":"Enterprise","price":"Custom"}]}'
  );

-- 为 'val' 列中的特定元素创建虚拟列。
CREATE VIRTUAL COLUMN (
  val ['name'],                 -- 提取 'name' 字段。
  val ['tags'] [0],             -- 提取 'tags' 数组中的第一个元素。
  val ['pricings'] [0] ['type'] -- 提取 'pricings' 数组中第一个定价的 'type' 字段。
) FOR test;

REFRESH VIRTUAL COLUMN FOR test;
```