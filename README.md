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