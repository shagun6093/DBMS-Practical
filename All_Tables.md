
# Creating Tables

### Client_master Table
#### create table:
```sql
CREATE TABLE Client_master (
  Client_no varchar(6) PRIMARY KEY, 
  Name varchar(25) NOT NULL, 
  Address1 varchar(20), 
  Address2 varchar(20), 
  City varchar(15), 
  Pincode numeric(8), 
  State varchar(15), 
  Bal_due numeric(10, 2),
  CHECK (Client_no like 'C%')
);
```
#### insert data
```sql
INSERT INTO Client_master VALUES ('C00001','Ivan Bayross',' ',' ','Bombay',400054,'Maharashtra', 15000);
INSERT INTO Client_master VALUES ('C00002','Vandana Saitwal',' ',' ','Madras',780001, 'Tamil Nadu',0);
INSERT INTO Client_master VALUES ('C00003','Pramada Jaguste', ' ', ' ', 'Bombay', 400057, 'Maharashtra', 5000);
INSERT INTO Client_master VALUES ('C00004','Basu Navindgi', ' ', ' ', 'Bombay', 400056, 'Maharashtra',0);
INSERT INTO Client_master VALUES ('C00005','Ravi Sreedharam',' ', ' ', 'Delhi', 110001, ' ',2000);
INSERT INTO Client_master VALUES ('C00006','Rukmini',' ', ' ', 'Bombay', 400050, 'Maharashtra',0);
```

### Product_master

#### create table
```sql
CREATE TABLE product_master (
  Product_no VARCHAR(6) PRIMARY KEY, 
  Description VARCHAR(50) NOT NULL, 
  Profit_percent NUMERIC(5,2) NOT NULL, 
  Unit_measure VARCHAR(10) NOT NULL, 
  Qty_on_hand NUMERIC(8) NOT NULL, 
  Reorder_lvl NUMERIC(8) NOT NULL, 
  Sell_price NUMERIC(8,2) NOT NULL, 
  Cost_price NUMERIC(8,2) NOT NULL,
  CHECK (Product_no like 'P%'),
  CHECK (Sell_price !=0),
  CHECK (Cost_price !=0)
);
```

#### insert data

```sql
INSERT INTO Product_master VALUES ('P00001','1.44 Floppies',5,'Piece',100,20,525,500);
INSERT INTO Product_master VALUES ('P03453','Monitors',6,'Piece',10,3,12000,11200);
INSERT INTO Product_master VALUES ('P06734','Mouse',5,'Piece',20,5,1050,1000); 
INSERT INTO Product_master VALUES ('P07865','1.22 Floppies',5,'Piece',100,20,525,500);
INSERT INTO Product_master VALUES ('P07868','Keyboards',2,'Piece',10,3,3150,3050); 
INSERT INTO Product_master VALUES ('P07885','CD Drive',2.5,'Piece',10,3,5250,5100);
INSERT INTO Product_master VALUES ('P07965','540 HDD',4,'Piece',10,3,8400,8000); 
INSERT INTO Product_master VALUES ('P07975','1.44 Drive',5,'Piece',10,3,1050,1000);
INSERT INTO Product_master VALUES ('P08865','1.22 Drive',5,'Piece',2,3,1050,1000);
```

### Salesman_master
#### create table
```sql
CREATE TABLE salesman_master (
  Salesman_no VARCHAR(6) PRIMARY KEY, 
  Salesman_name VARCHAR(20) NOT NULL, 
  Address1 VARCHAR(30) NOT NULL, 
  Address2 VARCHAR(30), 
  City VARCHAR(20), 
  PinCode VARCHAR(6), 
  State VARCHAR(20), 
  Sal_amt NUMERIC(8,2) NOT NULL, 
  Tgt_to_get NUMERIC(6,2) NOT NULL, 
  Ytd_sales NUMERIC(6,2) NOT NULL, 
  Remarks VARCHAR(60), 
  CHECK (Salesman_no LIKE 'S%'),
  CHECK (Sal_amt !=0),
  CHECK (Tgt_to_get !=0)
);
```
#### insert data
```sql
INSERT INTO salesman_master VALUES ('S00001','Kiran','A/14','Worli','Bombay','400002','Maharashtra',3000,100,50,'Good');  
INSERT INTO salesman_master VALUES ('S00002','Manish','65','Nariman','Bombay','400001','Maharashtra',3000,200,100,'Good');     
INSERT INTO salesman_master VALUES ('S00003','Ravi','P-7','Bandra','Bombay','400032','Maharashtra',3000,200,100,'Good');        
INSERT INTO salesman_master VALUES ('S00004','Ashish','A/5','Juhu','Bombay','400044','Maharashtra',3000,200,150,'Good');        
```

### Sales_order

#### create table
```sql
create table sales_order
(s_order_no varchar(6) PRIMARY KEY CHECK(s_order_no like 'O%'),
s_order_date date,
client_no varchar (6) references Client_master(client_no),
dely_add varchar(25),
salesman_no varchar(6) references salesman_master(salesman_no),
dely_type char(1) check(dely_type IN ('P','F')),
bill_yn char(1),
dely_date date,
check(dely_date > s_order_date),
order_status varchar (10) check (order_status IN ('IP','F','BO','C'))
);
```

#### insert data
```sql
insert into sales_order(s_order_no, s_order_date, client_no, dely_add, bill_yn, salesman_no, dely_date, order_status) values
('O19001', '1996-01-12', 'C00001', 'F', 'N', 'S00001', '1996-01-20', 'IP'),
('O19002', '1996-01-25', 'C00002', 'P', 'N', 'S00002', '1996-01-27', 'C'),
('O46865', '1996-02-18', 'C00003', 'F', 'Y', 'S00003', '1996-02-20', 'F'),
('O19003', '1996-04-03', 'C00001', 'F', 'Y', 'S00001', '1996-04-07', 'F'),
('O46866', '1996-05-20', 'C00004', 'P', 'N', 'S00002', '1996-05-22', 'C'),
('O10008', '1996-05-24', 'C00005', 'F', 'N', 'S00004', '1996-05-26', 'IP');
```
### Sales order detail

#### create table

```sql
create table sales_order_details
(
 s_order_no varchar(6) references sales_order(s_order_no),
 product_no varchar(6) references product_master(product_no),
 qty_ordered numeric(8),
 qty_disp numeric(8),
 product_rate numeric(10,2)
);
```
#### insert data
```sql
INSERT INTO sales_order_details VALUES ('O19001','P00001',4,4,525);  
INSERT INTO sales_order_details VALUES ('O19001','P07965',2,1,8400);  
INSERT INTO sales_order_details VALUES ('O19001','P07885',2,1,5250);  
INSERT INTO sales_order_details VALUES ('O19002','P00001',10,0,525);  
INSERT INTO sales_order_details VALUES ('O46865','P07868',3,3,3150);  
INSERT INTO sales_order_details VALUES ('O46865','P07885',3,1,5250);  
INSERT INTO sales_order_details VALUES ('O46865','P00001',10,10,525);  
INSERT INTO sales_order_details VALUES ('O46865','P03453',4,4,1050);  
INSERT INTO sales_order_details VALUES ('O19001','P03453',2,2,1050);  
INSERT INTO sales_order_details VALUES ('O19001','P06734',1,1,12000);  
INSERT INTO sales_order_details VALUES ('O19001','P07965',1,0,8400);  
INSERT INTO sales_order_details VALUES ('O19001','P07975',1,0,1050);  
INSERT INTO sales_order_details VALUES ('O19001','P00001',10,5,525);  
INSERT INTO sales_order_details VALUES ('O19001','P07975',5,3,1050);
```

### Challan header
#### create table
```sql
CREATE TABLE challan_header (
 challan_no VARCHAR(6) PRIMARY KEY check(challan_no like 'CH%'),
 s_order_no VARCHAR(6) REFERENCES sales_order(s_order_no),
 challan_date DATE NOT NULL,
 billed_yn CHAR(1) 
);
```
#### insert data
```sql
INSERT INTO challan_header VALUES ('CH9001','O19001','1995-12-12','Y');
INSERT INTO challan_header VALUES ('CH6865','O46865','1995-11-12','Y');
INSERT INTO challan_header VALUES ('CH3965','O10008','1995-10-12','Y');

```

### Challan header details
#### create table

```sql
CREATE TABLE challan_details (
 challan_no VARCHAR(6) REFERENCES challan_header(challan_no),
 product_no VARCHAR(6) REFERENCES product_master(product_no),
 qty_disp NUMERIC(8)
);
```
#### insert data

```sql
INSERT INTO challan_details VALUES ('CH9001','P00001',4);
INSERT INTO challan_details VALUES ('CH9001','P07965',1);
INSERT INTO challan_details VALUES ('CH9001','P07885',1);
INSERT INTO challan_details VALUES ('CH6865','P07868',3);
INSERT INTO challan_details VALUES ('CH6865','P03453',4);
INSERT INTO challan_details VALUES ('CH6865','P00001',10);
INSERT INTO challan_details VALUES ('CH3965','P00001',5);
INSERT INTO challan_details VALUES ('CH3965','P07975',2);

```
