# Sql-Session-2
Data Manipulation and Transformation: Altered database structure using Data Definition Language (DDL) commands, creating backups and setting primary keys. Ensured data integrity by converting date formats and handling null entries. Cleaned data by removing entries with 'Anonymous' names and filtering out specific phone numbers.
# Data Manipultion and Data Transformation
# Data Manipultion: used to modify or handle data, ensuring it is in right format in a accessible,
# organized and valuable for analysis
# DDL = Data Definition Language =the set of sql commands that deal with structuring of databases
# creating new database object = rows , columns
# modify existing database object
# delete database objects 


# create table
create table customer_backup as select * from customer;
create table billing_backup as select* from billing;
set sql_safe_update=0; # security measure =safe updates mode - you will have to employ conditions - that is where clause
# it will helps us in ddl comanding query
alter table customer add primary key(customer_id); # it will helps us to make customer_id as primary key
alter table customer modify customer_id int auto_increment;

# Practise
#set billing table in it billing_id as primary key and auto increment
alter table billing add primary key(bill_id);
alter table billing modify bill_id int auto_increment;



# subscription _date
update customer set Subscriptin_Date = str_to_date(Subscription_Date,"%m/%d/%Y");
alter table customer modify Subscription_Date datetime;

update customer set Date_of_Birth = str_to_date(Date_of_Birth,"%m/%d/%Y");
alter table customer modify Date_of_Birth datetime;

update customer set last_interaction_date = str_to_date(last_interaction_date,"%m/%d/%Y");
alter table customer modify last_interaction_date datetime;


select *
from customer
 where Subscription_Date is null and last_interaction_date is null;
 
 select *
from customers_backup
 where Subscription_Date is null and last_interaction_date is null;
 
 delete from customer where Subscription_Date is null and last_interaction_date is null;
 #erase all customers named anonymous
 
 #delete all entries in the billing table where the due date is before 
 #2022-01-01
 
 delete from customer where first_name = 'Anonymous';
 
 delete from billing where due_date < '2022-01-01';
 
 #Data Cleaning 
 
 select *
 from customer
 where phone_number not like '555%';
