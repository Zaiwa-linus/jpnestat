---
title: 日本の空き家数ランキング
---

# 日本の空き家数ランキング

以下のグラフは、日本の各都道府県の空き家数と空き家率を表示しています。
空き家率は、各都道府県の総住宅数に対する空き家数の割合として計算されています。

## 空き家数が多い上位10都道府県

```sql top10_vacant_houses
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
  vacant_houses DESC
LIMIT 10
```

<BarChart 
  data={top10_vacant_houses} 
  x="prefecture" 
  y="vacant_houses"
  y2="vacancy_rate"
  y2SeriesType="line"
  y2Title="空き家率"
  title="空き家数が多い上位10都道府県"
  xAxisTitle="都道府県"
  yAxisTitle="空き家数"
  y2AxisNumberFormat=".1%"
  xAxisLabelRotation={45}
  sort="y"
  sortOrder="desc"
/>

## 空き家数が少ない下位10都道府県

```sql bottom10_vacant_houses
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
  vacant_houses ASC
LIMIT 10
```

<BarChart 
  data={bottom10_vacant_houses} 
  x="prefecture" 
  y="vacant_houses"
  y2="vacancy_rate"
  y2SeriesType="line"
  y2Title="空き家率"
  title="空き家数が少ない下位10都道府県"
  xAxisTitle="都道府県"
  yAxisTitle="空き家数"
  y2AxisNumberFormat=".1%"
  xAxisLabelRotation={45}
  sort="y"
  sortOrder="asc"
/>

## データについて

このデータは、2023年10月に調査された「居住世帯の有無(9区分)別住宅数－全国、都道府県、21大都市」を加工して作成ています。

なお、データの取得は https://github.com/Zaiwa-linus/e-stat-adaptor を使用しています。

