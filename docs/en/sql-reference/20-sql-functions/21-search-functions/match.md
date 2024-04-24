---
title: MATCH
---
import FunctionDescription from '@site/src/components/FunctionDescription';

<FunctionDescription description="Introduced or updated: v1.2.425"/>

MATCH is an inverted index search function used to match the rows that meets the query string conditions. Please note that MATCH function can be only used in a where clause for filter.

## Syntax

```sql
MATCH( <query_fields>, <query_string> )
```

`query_fields` have two forms. One specifies a single query field and the other one specifies multiple fields with optional boost values.

`query_string` is a set of query terms without syntax; to support richer query syntax, use the [QUERY](query.md) function.

## Examples

```sql

CREATE TABLE test(title STRING, body STRING);

CREATE INVERTED INDEX idx ON test(title, body);

INSERT INTO test VALUES
('The Importance of Reading', 'Reading is a crucial skill that opens up a world of knowledge and imagination.'),
('The Benefits of Exercise', 'Exercise is essential for maintaining a healthy lifestyle.'),
('The Power of Perseverance', 'Perseverance is the key to overcoming obstacles and achieving success.'),
('The Art of Communication', 'Effective communication is crucial in everyday life.'),
('The Impact of Technology on Society', 'Technology has revolutionized our society in countless ways.');

SELECT * FROM test WHERE MATCH(title, 'art power');

┌────────────────────────────────────────────────────────────────────────────────────────────────────┐
│           title           │                                  body                                  │
├───────────────────────────┼────────────────────────────────────────────────────────────────────────┤
│ The Power of Perseverance │ Perseverance is the key to overcoming obstacles and achieving success. │
│ The Art of Communication  │ Effective communication is crucial in everyday life.                   │
└────────────────────────────────────────────────────────────────────────────────────────────────────┘

SELECT *, score() FROM test WHERE MATCH('title, body', 'knowledge technology');

┌──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┐
│                title                │                                      body                                      │  score()  │
├─────────────────────────────────────┼────────────────────────────────────────────────────────────────────────────────┼───────────┤
│ The Importance of Reading           │ Reading is a crucial skill that opens up a world of knowledge and imagination. │ 1.1550591 │
│ The Impact of Technology on Society │ Technology has revolutionized our society in countless ways.                   │ 2.6830134 │
└──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┘

SELECT *, score() FROM test WHERE MATCH('title^5, body^1.2', 'reading everyday');

┌────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┐
│           title           │                                      body                                      │  score()  │
├───────────────────────────┼────────────────────────────────────────────────────────────────────────────────┼───────────┤
│ The Importance of Reading │ Reading is a crucial skill that opens up a world of knowledge and imagination. │  8.585282 │
│ The Art of Communication  │ Effective communication is crucial in everyday life.                           │ 1.8575745 │
└────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┘
```
