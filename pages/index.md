---
title: 日本の空き家率ランキング
---

# 日本の空き家率ランキング（全都道府県）

以下のグラフは、日本の各都道府県の空き家率を空き家率が高い順に表示しています。
空き家率は、各都道府県の総住宅数に対する空き家数の割合として計算されています。

```sql vacancy_rate_ranking
SELECT
  t1.jp_area as prefecture,
  t2.value as vacant_houses,
  t1.value as total_houses,
  CAST(t2.value as FLOAT) / t1.value as vacancy_rate
FROM
  (SELECT jp_area, value FROM estat_csv.brank_house WHERE type = '総数') t1
  JOIN
  (SELECT jp_area, value FROM estat_csv.brank_house WHERE type = '空き家') t2
  ON t1.jp_area = t2.jp_area
ORDER BY
  vacancy_rate DESC
```

<BarChart 
  data={vacancy_rate_ranking} 
  x="prefecture" 
  y="vacancy_rate"
  swapXY={true}
  title="都道府県別空き家率ランキング"
  xAxisTitle="空き家率"
  yAxisTitle="都道府県"
  xAxisNumberFormat=".1%"
/>

## データについて

このデータは、各都道府県の総住宅数と空き家数から計算されています。
空き家率 = 空き家数 ÷ 総住宅数
