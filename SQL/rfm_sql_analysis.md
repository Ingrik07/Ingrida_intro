```sql
fm AS ( --frequency and monetary
SELECT
CustomerID,
COUNT(DISTINCT(invoiceNo)) AS frequency,
DATE_TRUNC(MAX(InvoiceDate), DAY) AS last_purchase,
SUM(Quantity * UnitPrice) AS monetary
FROM
`tc-da-1.turing_data_analytics.rfm`
WHERE
(CustomerID IS NOT NULL
AND UnitPrice > 0
AND Quantity > 0)
AND InvoiceDate <= '2011-12-01'
GROUP BY
CustomerID),

--recency
rec AS (
SELECT
*,
DATE_DIFF(DATE('2011-12-01'), DATE(last_purchase), DAY) AS recency
FROM
fm),
q AS (
--All percentiles for MONETARY
SELECT
*,
b.percentiles[
OFFSET
(25)] AS m25,
b.percentiles[
OFFSET
(50)] AS m50,
b.percentiles[
OFFSET
(75)] AS m75,
b.percentiles[
OFFSET
(100)] AS m100,
--All percentiles for FREQUENCY
c.percentiles[
OFFSET
(25)] AS f25,
c.percentiles[
OFFSET
(50)] AS f50,
c.percentiles[
OFFSET
(75)] AS f75,
c.percentiles[
OFFSET
(100)] AS f100,
--All percentiles for RECENCY
d.percentiles[
OFFSET
(25)] AS r25,
d.percentiles[
OFFSET
(50)] AS r50,
d.percentiles[
OFFSET
(75)] AS r75,
d.percentiles[
OFFSET
(100)] AS r100
FROM
rec a,
(
SELECT
APPROX_QUANTILES(monetary, 100) percentiles
FROM
rec) b,
(
SELECT
APPROX_QUANTILES(frequency, 100) percentiles
FROM
rec) c,
(
SELECT
APPROX_QUANTILES(recency, 100) percentiles
FROM
rec) d ),
score AS (
SELECT
*,
CAST(ROUND((f_score + m_score) / 2, 0) AS INT64) AS fm_score
--Calculate common RFM score
FROM (
SELECT
*,
CASE
WHEN monetary <= m25 THEN 1
WHEN monetary > m25
AND monetary <= m50 THEN 2
WHEN monetary <= m75 AND monetary > m50 THEN 3
WHEN monetary <= m100
AND monetary > m75 THEN 4
END
AS m_score,
CASE
WHEN frequency <= f25 THEN 1
WHEN frequency <= f50
AND frequency > f25 THEN 2
WHEN frequency <= f75 AND frequency > f50 THEN 3
WHEN frequency <= f100
AND frequency > f75 THEN 4
END
AS f_score,
--Recency scoring is reversed
CASE
WHEN recency <= r25 THEN 4
WHEN recency <= r50
AND recency > r25 THEN 3
WHEN recency <= r75 AND recency > r50 THEN 2
WHEN recency <= r100
AND recency > r75 THEN 1
END
AS r_score,
FROM
q))

--Segment customers into Best Customers, Loyal Customers, Big Spenders, Lost Customers and other categories

SELECT
DISTINCT CustomerID,
recency,
frequency,
monetary,
r_score,
f_score,
m_score,
fm_score,
CASE
WHEN (r_score = 4 AND fm_score = 4) OR (r_score = 4 AND fm_score = 3) OR (r_score = 3 AND fm_score = 4) THEN 'Best Customers'
WHEN (r_score = 4
AND fm_score =3)
OR (r_score = 3
AND fm_score = 3) THEN 'Loyal Customers'
WHEN (m_score = 4 AND fm_score = 4) OR (m_score = 3 AND fm_score = 4) OR (m_score = 4 AND fm_score = 3) THEN 'Big Spenders'
WHEN (r_score = 4
AND fm_score = 1)
OR (r_score = 4
AND fm_score = 2)
OR (r_score = 3
AND fm_score = 3)
OR (r_score = 3
AND fm_score = 2)
OR (r_score = 3
AND fm_score = 1) THEN 'Recent Customers'
WHEN (r_score = 4 AND fm_score = 2) OR (r_score = 2 AND fm_score = 4) OR (r_score = 2 AND fm_score = 3) THEN 'Promising Customers'
WHEN (r_score = 1
AND fm_score = 4)
OR (r_score = 1
AND fm_score = 3)
OR (r_score = 2
AND fm_score = 2) THEN 'Cant Lose Them'
WHEN (r_score = 1 AND fm_score = 1) OR (r_score = 2 AND fm_score = 1) OR (r_score = 1 AND fm_score = 2) THEN 'Lost Customers'
END
AS rfm_segment
FROM
score
ORDER BY
CustomerID;
```
