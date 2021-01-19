---
template: post
title: Applying Distinct and Dense_Rank to get first N distinct rows for each
  values of Column in SQL
slug: /posts/apply-distinct-and-dense_rank-in-sql
draft: false
priority: 1
date: 2021-01-04T16:28:09.507Z
description: Recently I came up with a problem statement where I had to filter
  my data to retrieve the first 3 distinct rows for each value of a certain
  column in SQL. I applied a Distinct and Dense Rank function to achieve this. I
  have explained every bit of the query in this post.
category: Programming
tags:
  - sql
  - relational database
  - database
  - dense_rank
  - distinct
  - partition
---
Recently I came up with a problem statement where I had to filter my data to retrieve first 3 distinct rows for each value of a certain column in SQL. The input dataset seems to be as follows:

TableName: **TrackingData**

| TrackingNumber | City    | DeliveryStatus |
| -------------- | ------- | -------------- |
| 1              | NewYork | Delivered      |
| 1              | NewYork | Delivered      |
| 2              | NewYork | Delivered      |
| 3              | Seattle | Delivered      |
| 3              | Seattle | Delivered      |
| 3              | Seattle | NotDelivered   |
| 4              | Seattle | Delivered      |
| 5              | Chicago | Delivered      |
| 6              | Chicago | Delivered      |
| 7              | Chicago | NotDelivered   |
| 8              | Chicago | Delivered      |
| 9              | Chicago | Delivered      |

![applying-distinct-and-dense_rank-in-sql](/media/optimized-caspar-camille-rubin-fpkvu7rdmco-unsplash.jpg "applying-distinct-and-dense_rank-in-sql  ")

## Problem Statement

These are the conditions that I need to use to filter the datasets:

1.Tracking Numbers are specific to the Cities. One city can have multiple rows with the same tracking number but the same number cannot be assigned to another city

2.Output dataset should have distinct tracking numbers for each city.

3.The Delivery status should be "Delivered".

4. Maximum 3 rows can be there for each city.

Based on the above criteria the resultant dataset should look like the following:

| TrackingNumber | City    | DeliveryStatus | RowNumber |
| -------------- | ------- | -------------- | --------- |
| 5              | Chicago | Delivered      | 1         |
| 6              | Chicago | Delivered      | 2         |
| 8              | Chicago | Delivered      | 3         |
| 1              | NewYork | Delivered      | 1         |
| 1              | NewYork | Delivered      | 1         |
| 2              | NewYork | Delivered      | 2         |
| 3              | Seattle | Delivered      | 1         |
| 3              | Seattle | Delivered      | 1         |
| 4              | Seattle | Delivered      | 2         |

## Preparing the Dataset

`create table TrackingData (TrackingNumber int,City varchar,DeliveryStatus varchar);`

`Insert into TrackingData values`

`(1, 'NewYork', 'Delivered'),`

`(1, 'NewYork', 'Delivered'),`

`(2, 'NewYork', 'Delivered'),`

`(3, 'Seattle', 'Delivered'),`

`(3, 'Seattle', 'Delivered'),`

`(3, 'Seattle', 'NotDelivered'),`

`(4, 'Seattle', 'Delivered'),`

`(5, 'Chicago', 'Delivered'),`

`(6, 'Chicago', 'Delivered'),`

`(7, 'Chicago', 'NotDelivered'),`

`(8, 'Chicago', 'Delivered'),`

`(9, 'Chicago', 'Delivered');`

``

## First Glance to Select Query

`select * from (`

`select distinct *, DENSE_RANK() over (partition by City order by TrackingNumber) as 'RowNumber' from TrackingData where DeliveryStatus = 'Delivered') as newtable`

`where newtable.RowNumber <=3`

Looks complex? It's easier than what it looks at the first glance. Let's decompose the query and understand it on the chunk. We have mainly three criteria: Distinct, Delivered and max 3 rows.

First two criteria can be simply achieved with the following select statement:

`select Distinct * from TrackingData where DeliveryStatus = 'Delivered';`

| TrackingNumber | City    | DeliveryStatus |
| -------------- | ------- | -------------- |
| 1              | NewYork | Delivered      |
| 2              | NewYork | Delivered      |
| 3              | Seattle | Delivered      |
| 4              | Seattle | Delivered      |
| 5              | Chicago | Delivered      |
| 6              | Chicago | Delivered      |
| 8              | Chicago | Delivered      |
| 9              | Chicago | Delivered      |

So the above table consists of rows with Distinct TrackingNumber for each City which is successfully delivered.

Now, How can we get Maximum 3 rows for each City? As we see in the above table there are 4 rows for Chicago but the expected result is 3.

We are going to follow the following steps:

* Add a new index column for each row based on the Cities(like NewYork 1...n, Chicago 1...n)

  Select the top 3 rows based on the Index column

We can use the Dense_Rank function to assign a unique rank value to a distinct row for each group of data. We will use the Partition and Over function to group our data based on the city name as below:

`select *, DENSE_RANK() over (partition by City order by TrackingNumber) as 'RowNumber' from TrackingData;`

**Output**

| TrackingNumber | City    | DeliveryStatus | RowNumber |
| -------------- | ------- | -------------- | --------- |
| 5              | Chicago | Delivered      | 1         |
| 6              | Chicago | Delivered      | 2         |
| 7              | Chicago | NotDelivered   | 3         |
| 8              | Chicago | Delivered      | 4         |
| 9              | Chicago | Delivered      | 5         |
| 1              | NewYork | Delivered      | 1         |
| 1              | NewYork | Delivered      | 1         |
| 2              | NewYork | Delivered      | 2         |
| 3              | Seattle | Delivered      | 1         |
| 3              | Seattle | Delivered      | 1         |
| 3              | Seattle | NotDelivered   | 1         |
| 4              | Seattle | Delivered      | 2         |

As we see in the above table, the rank is specific to the city and the unique rank is given only for the distinct row. Same rows are having the same rank value.

Now, we can filter the data based on our RowNumber column to get the top 3 rows for each country as below:

`select * from (`

`select *,DENSE_RANK() over (partition by City order by TrackingNumber) as 'RowNumber' from TrackingData) as newTable where newTable.'RowNumber' <=3;`

**Output**

| TrackingNumber | City    | DeliveryStatus | RowNumber |
| -------------- | ------- | -------------- | --------- |
| 5              | Chicago | Delivered      | 1         |
| 6              | Chicago | Delivered      | 2         |
| 7              | Chicago | NotDelivered   | 3         |
| 1              | NewYork | Delivered      | 1         |
| 1              | NewYork | Delivered      | 1         |
| 2              | NewYork | Delivered      | 2         |
| 3              | Seattle | Delivered      | 1         |
| 3              | Seattle | Delivered      | 1         |
| 3              | Seattle | NotDelivered   | 1         |
| 4              | Seattle | Delivered      | 2         |

***Note: We cannot directly use the RowNumber in the where clause since it is a derived column and the column is created only after the where clause is executed based on logical processing order. So we need to use the derived tables.***

Finally, let's merge all our select statement into one to get the desired output.

`select * from (`

`select distinct *, DENSE_RANK() over (partition by City order by TrackingNumber) as 'RowNumber' from TrackingData where DeliveryStatus = 'Delivered') as newtable`

`where newtable.RowNumber <=3;`

**Output**

| TrackingNumber | City    | DeliveryStatus | RowNumber |
| -------------- | ------- | -------------- | --------- |
| 5              | Chicago | Delivered      | 1         |
| 6              | Chicago | Delivered      | 2         |
| 8              | Chicago | Delivered      | 3         |
| 1              | NewYork | Delivered      | 1         |
| 1              | NewYork | Delivered      | 1         |
| 2              | NewYork | Delivered      | 2         |
| 3              | Seattle | Delivered      | 1         |
| 3              | Seattle | Delivered      | 1         |
| 4              | Seattle | Delivered      | 2         |

I hope this was helpful to you. Please free to give feedback on comment section :).