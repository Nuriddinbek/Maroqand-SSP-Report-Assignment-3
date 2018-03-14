#Report
##Assignment 3

>####Table Invoice normalization
**Table is in BCNF:** 
***
Rule: *table should be in 3NF and for every functional dependency X->Y, X should be the super key of the table*
***
Cause: Since there is a trivial functional dependency for the super key *{id, order_id} - > id*, *{id, order_id} - > order_id*, this means that if we know id and order_id of invoice id of the invoice can be uniquely determined
vice-versa if we know the values of *id and order_id, order_id* can be uniquely determined.

>####Table Payments normalization
**Table is in BCNF:** 
***
Rule: table should be in 3NF and for every functional dependency X->Y, X should be the super key of the table
***
Cause: 


>####Table Orders normalization
**Table is NOW in 1NF:** 
***
Rule: table should hold only atomic values
***
Cause: since table attributes(all columns) hold single values, it is in the *1NF*
***
**Table is NOW in 2NF:** 
***
Rule: *table should be in 1NF and there should be no partial dependency*
***
Cause: table is in 1NF but since *id* is primary key, non-prime keys(*product_desc, product_name*...) are not dependent on *id*, *order_date&quantity* is dependent on *id*
***
Result:
```
1. id, order_date, quantity should be placed into Order table while primary keys of the table customer and product as foreign keys
2. cust_name, cust_country should be placed into customers table. Since cust_name cannot be primary key(duplications), cust_id set to be primary key of the table customer
3. product_name, product_desc and product_price should be placed into products table. Since product_name cannot be field-key, product_id set to be primary key of the table product 
```
Sketch:
>#####order
|    id      |    cust_id    |   product_id   |  order_date  |  quantity  |
|:--------- :|:-------------:|:--------------:|:------------:|:----------:|
|     1      |       10       |     100       | 2016-02-04   |    10      | 
|     2      |       20       |     200       | 2016-02-24   |    1       | 
|     3      |       30       |     300       | 2015-03-12   |    1       | 
|     4      |       40       |     400       | 2016-02-04   |    1       |

>#####customer
|     cust_id    |   cust_name   |  cust_country |
|:--------------:|:-------------:|:-------------:|
|       1        |  Marylis      |     CHN       | 
|       2        |  Gloria       |     ITA       | 
|       3        |  Clay         |     GBR       | 
|       4        |  Marylis      |     CHN       |

>#####product
|   product_id   | product_name |    product_desc | product_price |
|:--------------:|:------------:|:---------------:|:-------------:|
|        1       |  pname_120_  | pdesc_844_844   |    122.19     | 
|        2       |  pname_775   | pdesc_511_511   |    840.14     | 
|        3       |  pname_275_  | pdesc_136_136   |    335.16     | 
|        4       |  pname_970_  | pdesc_418_418   |    3.46       |

**Table is NOW in 3NF:** 
***
Rule: table should be in 2NF and there should be no transitive functional dependency
***
Cause: table is in 2NF and observed that there is no transitive dependency 
***

**Table is NOW in BCNF:** 
***
Rule: table should be in 3NF and for every functional dependency X->Y, X should be the super key of the table.
***
Cause: table is in 3NF and but since there is no any functional dependency on cust_id and product_id, they are placed into another table order and other attributes moved into order_description 
***

Sketch:
>#####order_description
|  order_id  |  order_date  |  quantity  |
|:--------- :|:------------:|:----------:|
|     1      | 2016-02-04   |    10      | 
|     2      | 2016-02-24   |    1       | 
|     3      | 2015-03-12   |    1       | 
|     4      | 2016-02-04   |    1       |


>#####order
|   order_id |    cust_id    |   product_id |
|:--------- :|:-------------:|:------------:|
|     1      |       10      |     100      | 
|     2      |       20      |     200      | 
|     3      |       30      |     300      | 
|     4      |       40      |     400      |


>#####orders
|      id    |  cust_name    |  cust_country  | order-date | product_name | product_desc  | product_price | quantity |
|:--------- :|:-------------:|:--------------:|:----------:|:------------:|:-------------:|:-------------:|:--------:|
| 256        | Marylis       |    CHN         | 2016-02-04 |  pname_120_  | pdesc_844_844 |     122.19    |     10   |
| 260        | Gloria        |    ITA         | 2016-02-24 |  pname_775   | pdesc_511_511 |     840.14    |     1    |
| 233        | Clay          |    GBR         | 2015-03-12 |  pname_275   | pdesc_136_136 |     335.16    |     1    | 
| 256        | Marylis       |    CHN         | 2016-02-04 |  pname_970   | pdesc_418_418 |     3.46      |     1    |
