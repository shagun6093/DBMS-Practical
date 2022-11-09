
# Basic Queries on Tables

## 1.Find out the names of all the clients

```sql
 Select Name from Client_master;
```
## 2.Print the entire Client_master Table
```sql
Select *from Client_master;
```

## 3.Retrieve list of names and cities of all the clients


```sql
 Select Name,City from Client_master;
```

## 4.Find the names of all clients having 'a' as the second letter in their names

```sql
Select Name from Client_master where Name like '_a%';
```

## 5. List the various products available from Product_master.

```sql
Select Description from Product_master;

```
## 6.Find out clients who stay in city whose second letter is 'a'
```sql
 Select Name, City from Client_master where City like'_a%';
```

## 7.Find list of all clients who stay in bombay orcity delhi or city madaras



```sql
Select Name,City from Client_master where City="Bombay" OR City="Delhi" OR City ="Madras";
```

## 8.List all clients who are located in 'Bombay'
```sql
Select Name,City from Client_master where City="Bombay";
```
## 9. Print the list of clients whose val_due are greater than value 10000.

```sql
Select Name,Bal_due from Client_master where Bal_due>10000;
```
## 10.Display order information for client_no'C00001' and 'C00002'.
```sql
 Select *from Client_master where client_no='C00001' OR Client_no = 'C00002';
```
## 11. Find the products with description as '1.44 drive ' and '1.22 drive'.
```sql
Select Product_no from product_master where Description ='1.44 Drive' OR Description = '1.22 Drive';
```

## 12. Find product whose selling price is greater than 2000 and less than or equal to 5000.
```sql
Select Product_no ,Description  from Product_master where Sell_price between 2000 AND 5000;
```
## 13.Find product whose selling price is more than 1500 and also find new selling price as original price *15.
```sql
Select Product_no, Description,Sell_price,Sell_price*15 AS original_price from Product_master where Sell_price >1500;

```
## 14. List of all orders that were cancelled in month of march.
```sql
Select *from sales_order where order_status = "C" AND s_order_date between '1996-03-01' AND '1996-03-31';
```

## 15. Count the total no.of orders.
```sql
Select count(*) from sales_order;
```
## 16 . Calculate the average price of all the products 
```sql
 Select  round (avg(Sell_price)) from Product_master;
```
## 17. Calculate the minimum price of the product.
```sql
select min(Sell_price) from product_master;
```

## 18. Determine the maximum and minimum product price .Rename the title as max_price and min_price respectively.
```sql
select min(Cost_price)  AS min_price, max(Cost_price) AS max_price from product_master;
```
## 19.Count the no .of product having price greater than  or equal to 1500
```sql
 Select count(*) from Product_master where Sell_price>=1500;
```
## 20. Find all products whose qty_on_hand is less than reorder level.
```sql
Select Description from Product_master where qty_on_hand <reorder_lvl;
```
## 21. Count no of product whose qty_on_hand is less than reorder level.
```sql
Select count(*) from Product_master where qty_on_hand <reorder_lvl;
```
## 22. Display order info of orders placed in January
```sql
SELECT s_order_no,s_order_date FROM sales_order
WHERE s_order_date  LIKE '__%01%'; 
```
## 23. Display names having 'A' as the second alphabet
```sql
Select Name from CLient_master where Name like '_A%';
```
## 24.Display client no and bal_due and arrange bal_due in decreasing/descending order
```sql
 Select Bal_due,Client_no from Client_master order by Client_no desc;
 ```
 ## 25.Display client names, city and arrange client names in alphabetical order
```sql
Select Name,City from Client_master order by Name;
```
