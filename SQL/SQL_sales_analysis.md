SQL RFM task:
1. Calculate recency, frequency and money value and convert those values into R, F and M scores by using Quartiles.
2. Calculate common RFM score.
3. Segment customers into Best Customers, Loyal Customers, Big Spenders, Lost Customers and other categories

```sql
--Creating CUSTOMER table
WITH
  order_value AS (
  SELECT
    SalesOrderID,
    AVG(TotalDue) AS avg_order_value,
    CustomerID
  FROM
    `tc-da-1.adwentureworks_db.salesorderheader`
  GROUP BY
    1,
    3 ),
  customer_orders_count AS (
  SELECT
    CustomerID,
    COUNT(DISTINCT(SalesOrderID)) AS orders_count
  FROM
    `tc-da-1.adwentureworks_db.salesorderheader`
  GROUP BY
    CustomerID ),
  cust_loyalty AS (
  SELECT
    CustomerID,
    COUNT(SalesOrderID),
    CASE
      WHEN COUNT(SalesOrderID) = 1 THEN 'One-Time'
      WHEN COUNT(SalesOrderID) <= 3
    AND COUNT(SalesOrderID) > 1 THEN '2-3'
    ELSE
    '4+'
  END
    AS customer_loyalty
  FROM
    `tc-da-1.adwentureworks_db.salesorderheader`
  GROUP BY
    CustomerID )
SELECT
  cu.CustomerID AS CustomerID,
  sales.SalesOrderID,
  ad.City AS City,
  st.Name AS State,
  co_reg.Name AS Country,
  custorders.orders_count,
  ordervalue.avg_order_value AS aov,
  reason.Name as Sales_reason,
  ROUND(SUM(sales.TotalDue), 3) AS total_amount,
  MAX(OrderDate) AS date_last_order,
  CASE
    WHEN DATETIME(MAX(OrderDate)) > ( SELECT DATETIME_ADD(CAST(MAX(OrderDate) AS DATETIME), INTERVAL -365 DAY) FROM `tc-da-1.adwentureworks_db.salesorderheader`) THEN 'ACTIVE'
  ELSE
  'INACTIVE'
END
  ACTIVITY
FROM
  `tc-da-1.adwentureworks_db.customer` AS cu
INNER JOIN
  `tc-da-1.adwentureworks_db.customeraddress` AS cust_ad
ON
  cust_ad.CustomerID = cu.CustomerID
INNER JOIN
  `tc-da-1.adwentureworks_db.address` AS ad
ON
  ad.AddressID = cust_ad.AddressID
INNER JOIN
  `tc-da-1.adwentureworks_db.stateprovince` AS st
ON
  st.StateProvinceID = ad.StateProvinceID
INNER JOIN
  `tc-da-1.adwentureworks_db.countryregion` AS co_reg
ON
  co_reg.CountryRegionCode = st.CountryRegionCode
INNER JOIN
  `tc-da-1.adwentureworks_db.salesorderheader` AS sales
ON
  sales.CustomerID = cu.CustomerID
  FULL JOIN `tc-da-1.adwentureworks_db.salesorderheadersalesreason` as sales_reas
  ON sales_reas.SalesOrderID = sales.SalesOrderID
  FULL JOIN `tc-da-1.adwentureworks_db.salesreason` as reason
  ON reason.SalesReasonID = sales_reas.SalesReasonID
INNER JOIN
  order_value AS ordervalue
ON
  sales.SalesOrderID = ordervalue.SalesOrderID
INNER JOIN
  customer_orders_count AS custorders
ON
  custorders.CustomerID = sales.CustomerID
  INNER JOIN
  customer_orders_count as loyalty
  ON
  loyalty.CustomerID = cu.CustomerID
GROUP BY
  1,
  2,
  3,
  4,
  5,
  6,
  7,
  8
ORDER BY
  cu.CustomerID;

-- Sales reason table
WITH sales_per_reason AS (
 SELECT
  sales.SalesOrderID as  SalesOrderID,
   DATE_TRUNC(sales.OrderDate, MONTH) AS year_month,
   sales_reason.SalesReasonID,
   SUM(sales.TotalDue) AS sales_amount
 FROM
   `tc-da-1.adwentureworks_db.salesorderheader` AS sales
 INNER JOIN
   `tc-da-1.adwentureworks_db.salesorderheadersalesreason` AS sales_reason
 ON
   sales.SalesOrderID = sales_reason.salesOrderID
 GROUP BY 1,2,3
)
SELECT
 sales_per_reason.SalesOrderID,
 product.ProductID,
 sales_per_reason.year_month,
 reason.Name AS sales_reason,
 sales_per_reason.sales_amount
FROM
 sales_per_reason
LEFT JOIN
 `tc-da-1.adwentureworks_db.salesreason` AS reason
ON
 sales_per_reason.SalesReasonID = reason.SalesReasonID
 LEFT JOIN `tc-da-1.adwentureworks_db.salesorderdetail` as detail
 on sales_per_reason.SalesOrderID = detail.SalesOrderID
 LEFT JOIN `tc-da-1.adwentureworks_db.product` as product
 ON product.ProductID = detail.ProductID;

--Product/country table
SELECT
  salesorderheader.*,
  province.stateprovincecode as ship_province,
  province.CountryRegionCode as country_code,
  province.name as country_state_name,
  product.ProductID as ProductID,
  product.name as ProductName
FROM
  `tc-da-1.adwentureworks_db.salesorderheader` AS salesorderheader
  INNER JOIN `tc-da-1.adwentureworks_db.address` as address
  ON salesorderheader.ShipToAddressID = address.AddressID
  INNER JOIN `tc-da-1.adwentureworks_db.stateprovince` as province
  ON address.stateprovinceid = province.stateprovinceid
  INNER JOIN `tc-da-1.adwentureworks_db.salesorderdetail` as salesorderdetail
  ON salesorderdetail.SalesOrderID = salesorderheader.SalesOrderID
  INNER JOIN `tc-da-1.adwentureworks_db.product` as product
  ON product.ProductID = salesorderdetail.ProductID;

--Map geo table
SELECT
      salesorderheader.*,
      province.stateprovincecode as ship_province,
      province.CountryRegionCode as country_code,
      province.name as country_state_name
FROM `tc-da-1.adwentureworks_db.salesorderheader` as salesorderheader
INNER JOIN
     `tc-da-1.adwentureworks_db.address` as address
    ON salesorderheader.ShipToAddressID = address.AddressID
INNER JOIN
     `tc-da-1.adwentureworks_db.stateprovince` as province
    ON address.stateprovinceid = province.stateprovinceid

```
