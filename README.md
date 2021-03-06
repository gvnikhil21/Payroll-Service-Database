# Payroll-Service-Database

### Create payroll_service database
```
create database payroll_service;
```
### View all databases
```
show databases;
```
### Switch to payroll_service database
```
use payroll_service;
```
### Create table employee_payroll
```
create table employee_payroll(
id 		int unsigned not null auto_increment,
name 		varchar(30) not null,
start		date not null,
salary		double not null,
primary key 	(id)
);
```
### View tables in payroll_service database
```
show tables;
```
### View payroll_serivce database's field formats
```
describe employee_payroll;
```
### Insert values into employee_payroll table
```
insert into employee_payroll (name, start, salary) values
('Gates', '2018-01-03', 1000000),
('Mark', '2019-11-13', 2000000),
('Charlie', '2020-05-21', 3000000);
```
### Retrieve all employee payroll data added to payroll_service database
```
select * from employee_payroll;
```
### Retrieve salary data for particular employee 
```
select salary from employee_payroll where name = 'Gates';
```
### Retrieve all the data for employee who joined in particular date range
```
select * from employee_payroll
where start between cast('2018-01-01' as date) and date(now());
```
### Add gender to employee_payroll table after name column
```
alter table employee_payroll
add gender char(1) not null after name;
```
### Update rows in table to reflect correct employee gender
#### Add gender as 'M' for male employees
```
update employee_payroll
set gender='M' 
where name='Gates' or name='Charlie';
```
#### Add gender as 'F' for female employees
```
update employee_payroll
set gender='F'
where name='Mark';
```
### Find sum of all the salaries present in employee_payroll table
```
select sum(salary) from employee_payroll;
```
### Find sum of salaries of male employees
```
select sum(salary) from employee_payroll
where gender='M';
```
### Find avg of all salaries
```
select avg(salary) from employee_payroll;
```
### Find avg salaries of male and female employees
```
select gender, avg(salary) from employee_payroll
group by gender;
```
### Find max salary
```
select max(salary) from employee_payroll;
```
### Find min salary
```
select min(salary) from employee_payroll;
```
### Find count of male and female employees
```
select gender,count(gender) from employee_payroll
group by gender;
```
### Store employee phone, address, department
#### Add new columns to the employee_payroll table
```
alter table employee_payroll
add (phone bigint(10) not null, address varchar(30) default 'main-road', department varchar(20) not null);
```
### Extend employee_payroll table to have basic_pay, deductions, taxable_pay, income_tax, net_pay
```
alter table employee_payroll
add(basic_pay bigint(15) not null, deductions bigint(15) not null, taxable_pay bigint(15) not null, income_tax bigint(15) not null, net_pay bigint(15) not null);
```
### Add Terissa to sales and marketing department of employee_payroll table
```
alter table employee_payroll drop salary;

insert into employee_payroll values
(4,'Terissa','F','2020-05-22', 0,'abc', 'Sales', 4000000,0,0,0,0),
(5,'Terissa','F','2020-05-22', 0,'abc', 'Marketing', 4000000,2000000,2000000,500000,1500000);
```
### Create new schema following normalization concept
#### Drop employee_payroll table
```
drop table employee_payroll;
```
### Create ER-Model and convert to relational model by workbench
```
use of forward engineer option in workbench to create tables as per ER-Diagram
```
### Ensuring retrieval queries for new table structure
#### Retrieve all values from employee table and payroll table
```
select employee.*,basic_pay,deductions,taxable_pay,tax,net_pay from employee join payroll
on employee.employee_id=payroll.employee_id;
```
#### Retrieve basic_pay (salary) for particular employee
```
select employee.employee_id, employee.name, payroll.basic_pay from
employee join payroll
on employee.employee_id=payroll.employee_id
where employee.name='Gates';
```
### Perform operations with multirow/group functions
```
select sum(basic_pay) from payroll;

select employee.gender, sum(basic_pay) from 
employee join payroll
on employee.employee_id=payroll.employee_id
group by employee.gender;

select avg(salary) from payroll;

select employee.gender, avg(basic_pay) from 
employee join payroll
on employee.employee_id=payroll.employee_id
group by gender;

select max(basic_pay) from payroll;

select min(basic_pay) from payroll;

select gender, count(gender) from employee
group by gender;
```