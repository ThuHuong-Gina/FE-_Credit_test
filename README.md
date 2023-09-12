# FE Credit test
This is a test from FE credit about the transaction in e-commerce data

## Requirement: 
Please complete and send the answer back within 1 hour & 45 minutes, with 1 hour for Python Tool and 45 minutes for SQL Tool
1. Clean duplicated data and remove orders which have statuses (Fail, Cancelled, Lost and Returned)
2. Calculating the percentage of revenue of each brand and of each platform
3. Use python library to show/visualize revenue distribution by brand
4. Show revenue by month using appropriate visual charts and not in the table

### 1. SQL query 

#### Checking dataset

````
-- Check how many order in the dstaset
SELECT COUNT(id)  AS count_order
FROM [model].[guest].[FEcredit];
````
![image](https://github.com/ThuHuong-Gina/FE-_Credit_test/assets/141025228/b457adf6-ac8b-4e69-baef-dd3376cff81d)

```
-- Count how many distinct order id
SELECT COUNT(distinct id)  AS count_distinct
FROM [model].[guest].[FEcredit];
```
![image](https://github.com/ThuHuong-Gina/FE-_Credit_test/assets/141025228/136d7190-ac5b-4bc8-89fd-8d38b0df4785)

* Question 1. Clean duplicated data and remove orders which have statuses (Fail, Cancelled, Lost and Returned)
```
SELECT 
    DISTINCT *
FROM [model].[guest].[FEcredit]
WHERE [status] Not IN ('Fail', 'Canceled', 'Lost and Returned');
```
=> Result: top 10 rows 

![image](https://github.com/ThuHuong-Gina/FE-_Credit_test/assets/141025228/07bcc9f1-638a-4e01-99c9-fbaeda5af300)

* QuestionCalculating the percentage of revenue of each brand and of each platform
  
```
-- Checking how many branch
SELECT 
    DISTINCT branch
FROM [model].[guest].[FEcredit];
--Checking how many platform
SELECT 
    DISTINCT platform
FROM [model].[guest].[FEcredit];
-- Calculate 
SELECT
    branch,
    platform,
    SUM(selling_price) AS total_selling_price,
    SUM(selling_price) / (SUM(SUM(selling_price)) OVER (PARTITION BY branch)) * 100 AS percentage_of_branch_revenue,
    SUM(selling_price) / (SUM(SUM(selling_price)) OVER (PARTITION BY platform)) * 100 AS percentage_of_platform_revenue
FROM
    [model].[guest].[FEcredit]
GROUP BY
    branch, platform;
```
![image](https://github.com/ThuHuong-Gina/FE-_Credit_test/assets/141025228/f00bd2ac-60b4-4018-ae5d-cffc364c46a7)

![image](https://github.com/ThuHuong-Gina/FE-_Credit_test/assets/141025228/b0f8fa0e-9d2c-43d7-a25e-9c238a84a354)

2. Python Query 

