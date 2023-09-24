
CREATE TABLE Animal_habitate
(
animal_type varchar(100),
staff_id varchar(30),
breakfast_timimg int,
breakfast_food varchar(100),
breakfast_stock int,
lunch_timimg int,
lunch_food varchar(100),
lunch_stock int,
dinner_timimg int,
dinner_food varchar(100),
dinner_stock int,
PRIMARY KEY(animal_type),
--FOREIGN KEY (a_name) references Animal_details(a_name)
 );




CREATE TABLE Animal_details
(
animal_id varchar(100),
cage_no int,
animal_type varchar(100),
scientific_name varchar(100),
gender varchar(30),
gestation_month int,
present_health varchar(100),
birth_date date,
class varchar(100),
pictures varbinary(max),
PRIMARY KEY(animal_id),
FOREIGN KEY (animal_type) references Animal_habitate(animal_type)
 );

 
create table staff_details
( 
   staff_id varchar(100),
   staff_name varchar(100),
   gender varchar(100),
   job_type varchar(100),
   salary varchar(100),
   email_address varchar(100),
   shifting_time varchar(100) NOT NULL,
   date_of_joining date not null,
   job_duration varchar(100),
   primary key(staff_id)
);
create table manager_details
( 
   manager_id varchar(100),
   staff_id varchar(100),
  -- manager_name varchar(100),
  -- gender varchar(100),
  -- job_type varchar(100),
  -- salary varchar(100),
 --  email_address varchar(100),
   MANAGING_AREA VARCHAR(100)NOT NULL,
   MANAGING_EXPERIENCE INT NOT NULL,
   GENERAL_MANAGER_ENUM varchar(20),
   ADMIN_PRIVILAGES_ENUM varchar(20),
   primary key(manager_id),
   FOREIGN KEY (staff_id) references  staff_details(staff_id)
);
-- no need of this table
CREATE TABLE ANIMAL_Import
(
import_id VARCHAR(25) NOT NULL,
animal_id varchar(100) NOT NULL,
ENTRY1 DATE NOT NULL,
PLACE varchar (30) NOT NULL,
IMPORT_COST int NOT NULL,
AGE_DURING_EXPORT int NOT NULL,
PRIMARY KEY(import_id),
FOREIGN KEY (animal_id) references  Animal_details(animal_id)
);
CREATE TABLE expense
(
EXPENSE_ID varchar (30) NOT NULL,
animal_id varchar(100) NOT NULL,
FOOD_COST int NOT NULL,
MEDICINE_COST int NOT NULL,
CLEANING_COST int NOT NULL,
SERVICE_CHARGE varchar (30) NOT NULL,
PRIMARY KEY(EXPENSE_ID),
FOREIGN KEY (animal_id) references Animal_details(animal_id)
 );
 
Create table vet_details
(
   vet_id varchar(100),
   vet_name varchar(100),
   staff_id varchar(100),
   head_vet_enum varchar(20),
   speciality varchar(100),
   veternity_experience int not null,
   primary key(vet_id),
   FOREIGN KEY (staff_id) references staff_details(staff_id)
);

Create table visitor_details
(
   visitor_id varchar(100),
   age int,
   ticket_type_enum varchar(20),
   zoo_ticket_code varchar(100) ,
   museum_ticket_code varchar(100),
   ticket_price varchar(100),
   coupon_no varchar(100) UNIQUE,
   primary key(visitor_id)
);
Create table food_court
(
   coupon_no varchar(100),
   staff_id varchar(100),
   order_id varchar(100),
   food_type varchar(100),
   food_name varchar(100),
   price varchar(100),
   vat varchar(100),
   primary key(order_id),
   FOREIGN KEY (coupon_no) references visitor_details(coupon_no)
);
create table Zoo_Museum
(
Museum_Id varchar(100) not null,
Name varchar(30),
Type varchar(30),
Import_From varchar(30),
Year1 int ,
primary key (Museum_Id)
);
CREATE TABLE RECORD
(
RECORD_ID VARCHAR(25) NOT NULL,
cage_no varchar(100) ,
staff_id varchar (100),
visitor_id VARCHAR(100),
Museum_Id VARCHAR(100),
TYPE_OF_RECORD varchar (30) NOT NULL,
DATE_RECORD_CREATED date NOT NULL,
RECORD_DETAILS varchar (300) NOT NULL,
primary key(RECORD_ID),
--FOREIGN KEY (animal_id) references Animal_details(animal_id),
FOREIGN KEY (staff_id) references staff_details(staff_id),
FOREIGN KEY (visitor_id) references visitor_details(visitor_id),
FOREIGN KEY (Museum_Id) references Zoo_Museum(Museum_Id)
 );

 drop table if exists pecies_count;

 create table species_count(
 scintific_name varchar(100) PRIMARY KEY,
 count1 int);

 -- yyyy-mm-dd
 INSERT INTO Animal_habitate(animal_type, staff_id,breakfast_timimg,breakfast_food,breakfast_stock, lunch_timimg,lunch_food,lunch_stock,dinner_timimg,dinner_food,dinner_stock)
VALUES('Elephant','S-10001',9,'banana', 400 ,13,'bamboo',800,22,'hay',600),
('Hippopotamus','S-10002',9,'leaf', 400 ,13,'bamboo',800,22,'grass',600),
('Rhinocers','S-10003',9,'fruit', 400 ,13,'meat',800,22,'fish',600),
('Zebra','S-10004',9,'banana', 400 ,13,'grass',800,22,'hay',600),
('Giraffe','S-10005',9,'leaf', 400 ,13,'bamboo',800,22,'grass',600),
('Horse','S-10006',9,'sprouts', 400 ,13,'grass',800,22,'grass',600),
('Crocidile','S-10008',9,'meat', 400 ,13,'meat',800,22,'fish',600),
('Peacock','S-10010',9,'grass', 400 ,13,'insects',800,22,'hay',600),
('Deer','S-10011',9,'banana', 400 ,13,'grass',800,22,'hay',600),
('Python','S-10005',9,'insects', 400 ,13,'insects',800,22,'fruit',600),
('Tiger','S-10002',9,'meat', 400 ,13,'fish',800,22,'fruit',600),
('Lion','S-10001',9,'meat', 400 ,13,'fish',800,22,'fruit',600);

delete
from Animal_details;

INSERT INTO Animal_details(animal_id,cage_no,animal_type,gender, gestation_month,birth_date,class,scientific_name,present_health,pictures)
Values
('hippo 1',2,'Hippopotamus', 'F', 7, '2010-08-27', 'Chordata','Hippopotamus Amphibius','Good',(SELECT * FROM OPENROWSET(BULK N'C:\images\Hippopotamus.jpg', SINGLE_BLOB) as T1)),
('rhino 1',3,'Rhinocers', 'F', 16, '2010-03-26', 'Chordata','Rhinocerotidae','Good',(SELECT * FROM OPENROWSET(BULK N'C:\images\Rhino.jpg', SINGLE_BLOB) as T1)),
('zebra 1',4,'Zebra', 'F', 12, '2007-11-26', 'Chordata','Equus Quagga','Good',(SELECT * FROM OPENROWSET(BULK N'C:\images\Zebra.jpeg', SINGLE_BLOB) as T1)),
('girraf 1',5,'Giraffe', 'M', NULL, '2005-09-20', 'Chordata','Giraffa','Good',(SELECT * FROM OPENROWSET(BULK N'C:\images\Giraffe.jpg', SINGLE_BLOB) as T1)),
('horse 1',6,'Horse', 'F', 11, '2007-10-10', 'Chordata','Equus Caballus','good',(SELECT * FROM OPENROWSET(BULK N'C:\images\Horse.jpg', SINGLE_BLOB) as T1)),
('bd 1',7,'Deer', 'M', NULL, '2006-11-17', 'Chordata','Muntiacus','Good',(SELECT * FROM OPENROWSET(BULK N'C:\images\BarkingDeer.jpg', SINGLE_BLOB) as T1)),
('sd 1',7,'Deer', 'F', 6, '2007-07-20', 'Chordata','Axis Axis','Good',(SELECT * FROM OPENROWSET(BULK N'C:\images\SpottedDeer.jpeg', SINGLE_BLOB) as T1)),
('rbt 1',9,'Tiger', 'F', 3, '2006-05-03', 'Chordata',' Panthera Tigris Tigris','Sick',(SELECT * FROM OPENROWSET(BULK N'C:\images\RoyalBengalTiger.jpg', SINGLE_BLOB) as T1)),
('IL 1',10,'Lion', 'F', 3, '2006-05-03','Chordata',' Panthera Leo Persica','Good',(SELECT * FROM OPENROWSET(BULK N'C:\images\download.jpeg', SINGLE_BLOB) as T1)),
('bld 1',7,'Deer', 'M', NULL, '2005-09-20', 'Chordata','Ursus Americanus','Good',(SELECT * FROM OPENROWSET(BULK N'C:\images\BarkingDeer.jpg', SINGLE_BLOB) as T1)),
('crocodile 1',12,'Crocidile', 'F', 6, '2007-07-20', 'Reptile','Crocidylinae','Good',(SELECT * FROM OPENROWSET(BULK N'C:\images\Crocodile.jpg', SINGLE_BLOB) as T1)),
('python 1',13,'Python', 'F', 5, '2007-04-17', 'Reptile','Pythonidae','Good',(SELECT * FROM OPENROWSET(BULK N'C:\images\Python.jpg', SINGLE_BLOB) as T1)),
('peacock 1',14,'Peacock', 'F', 3, '2007-10-10', 'Aves','Pavo cristatus','Good',(SELECT * FROM OPENROWSET(BULK N'C:\images\Crocodile.jpg', SINGLE_BLOB) as T1));



insert into staff_details(staff_id, staff_name, gender, job_type, salary, email_address, shifting_time, date_of_joining, job_duration)
values
('S-10001','Abdul Alom','Male','Caretakeer','10,000tk','abdulalam707@gmail.com','Morning',CONVERT(DATETIME,'27-09-2000',103),'21 years'),
('S-10002','Salma Nahar','Female','Accountent','30,000tk','Salma@gmail.com','Evening',CONVERT(DATETIME,'10-01-2005',103),'16 years'),
('S-10003','Rahim Rahman','Male','Accountent','30,000tk','Rahim@gmail.com','Morning',CONVERT(DATETIME,'27-05-2008',103),'13 years'),
('S-10004','Abul Kashim','Male','Waiter','9,000tk','Abul@gmail.com','Morning',CONVERT(DATETIME,'02-02-2015',103),'6 years'),
('S-10005','Nurul Islam','Male','Canteen Cashier','13,000tk','Nurul54Islam@gmail.com','Morning',CONVERT(DATETIME,'10-01-2005',103),'16 years'),
('S-10006','Kashim','Male','Caretakeer','10,000tk','abdulalam707@gmail.com','Evening',CONVERT(DATETIME,'17-07-2001',103),'20 years'),
('S-10007','Mahfuz Sarkar','Male','Ticket-Seller','8,000tk','Mahfuz@gmail.com','Morning',CONVERT(DATETIME,'06-06-2003',103),'19 years'),
('S-10008','Hasan','Male','Accountent','30,000tk','Hasan@gmail.com','Morning',CONVERT(DATETIME,'06-06-2003',103),'19 years'),
('S-10009','Hasina','Female','Ticket-Seller','8,000tk','Hasina@gmail.com','Evening',CONVERT(DATETIME,'01-06-2017',103),'4 years'),
('S-10010','Rohima Akter','Female','Food Manager','40,000tk','Akter45@gmail.com','Morning',CONVERT(DATETIME,'15-09-2013',103),'8 years'),
('S-10011','Abdul','Male','Zoo Manager','41,000tk','Abdul@gmail.com','Morning',CONVERT(DATETIME,'02-02-2015',103),'6 years'),
('S-10012','Mollika Begum','Female','Cleaner','7,000tk','Mollika@gmail.com','Evening',CONVERT(DATETIME,'01-06-2017',103),'4 years'),
('S-10013','Hasan','Male','Waiter','9,000tk','abdulalam707@gmail.com','Morning',CONVERT(DATETIME,'15-09-2013',103),'8 years'),
('S-10014','Anik Islam','Male','Cleaner','9,000tk','AnikIslam@gmail.com','Evening',CONVERT(DATETIME,'17-07-2001',103),'20 years'),
('S-10015','Rohima Akter','Female','Kennel Assistant','10,000tk','Rohima@gmail.com','Morning',CONVERT(DATETIME,'15-09-2013',103),'8 years'),
('S-10016','Forhad','Male','Kennel Assistant','5,000tk','Forhad@gmail.com','Morning',CONVERT(DATETIME,'04-07-2012',103),'9 years'),
('S-10017','Forid','Male','Kennel Assistant','5,000tk','Forid@gmail.com','Morning',CONVERT(DATETIME,'02-02-2001',103),'20 years'),
('S-10018','Giash','Male','Kennel Assistant','5,000tk','Giash@gmail.com','Morning',CONVERT(DATETIME,'04-07-2012',103),'9 years'),
('S-10019','Rahima Akter','Female','Kennel Assistant','5,000tk','Rahima@gmail.com','Morning',CONVERT(DATETIME,'13-03-2004',103),'15 years'),
('S-10020','Tawhid Hossain','Male','Veterinarian','55,000tk','Tawhid@gmail.com','Morning',CONVERT(DATETIME,'04-07-2012',103),'9 years'),
('S-10021','Toriqul Islam','Male','Veterinarian','55,000tk','Toriqul@gmail.com','Evening',CONVERT(DATETIME,'16-04-2004',103),'17 years'),
('S-10022','Mirazul Rahman','Male','Veterinarian','55,000tk','Mirazul@gmail.com','Morning',CONVERT(DATETIME,'04-07-2012',103),'9 years'),
('S-10023','Mohammod anis','Male','Veterinarian','50,000tk','anis@gmail.com','Evening',CONVERT(DATETIME,'02-02-2010',103),'10 years'),
('S-10024','Rowshan Karim','Feale','Veterinarian','50,000tk','Rowshan@gmail.com','Morning',CONVERT(DATETIME,'02-02-2009',103),'11 years'),
('S-10025','Nurul Islam','Male','Veterinarian','50,000tk','Nurul@gmail.com','Morning',CONVERT(DATETIME,'23-05-2013',103),'8 years'),
('S-10026','Jui','Feale','Canteen Cashier','13,000tk','Jui@gmail.com','Evening',CONVERT(DATETIME,'10-10-2019',103),'2 years'),
('S-10027','Almas','Male','Canteen Cashier','13,000tk','Almas@gmail.com','Morning',CONVERT(DATETIME,'13-12-2016',103),'5 years'),
('S-10028','Fahim Alom','Male','Canteen Cashier','13,000tk','Fahim@gmail.com','Evening',CONVERT(DATETIME,'23-05-2013',103),'8 years'),
('S-10029','Farzina','Female','Caretakeer','10,000tk','Farzina87@gmail.com','Morning',CONVERT(DATETIME,'10-10-2019',103),'2 years'),
('S-10030','Mirazul Rahman','Male','Food Manager','40,000tk','Rahmanirazul@gmail.com','evening',CONVERT(DATETIME,'10-01-2002',103),'19 years'),
('S-10031','Sarkar','Male','Zoo Manager','41,000tk','abdulalam707@gmail.com','Evening',CONVERT(DATETIME,'23-05-2013',103),'8 years'),
('S-10032','Siddik Bosh','Male','Vet Manager','40,000tk','Sarkar@gmail.com','Morning',CONVERT(DATETIME,'07-07-2003',103),'17 years'),
('S-10033','Karim Rohman','Male','Vet Manager','40,000tk','Karim@gmail.com','Evening',CONVERT(DATETIME,'27-06-2000',103),'21 years');

insert into manager_details(manager_id,staff_id,MANAGING_AREA,MANAGING_EXPERIENCE,GENERAL_MANAGER_ENUM,ADMIN_PRIVILAGES_ENUM)
values('M-10001','S-10010','CANTEEN FOOD','10','YES','YES'),
('M-10002','S-10011','SECURITY','7','YES','YES'),
('M-10003','S-10030','ANIMAL FOOD','20','YES','YES'),
('M-10004','S-10031','ANIMAL CHECK','10','YES','NO'),
('M-10005','S-10032','ANIMAL HEALTH','17','YES','YES'),
('M-10006','S-10033','ANIMAL NUTRITION','24','NO','NO');


 
 INSERT INTO  ANIMAL_import(import_id, Animal_ID, ENTRY1,PLACE, IMPORT_COST, AGE_DURING_EXPORT)
VALUES ('G-303','girraf 1',CONVERT(DATETIME,'24-12-2016',103),'AFRICA',106000,23),
('G-304','horse 1',CONVERT(DATETIME,'24-12-2016',103),'AFRICA',06000.00,21),
('G-305','hippo 1',CONVERT(DATETIME,'01-11-2010',103),'UGANDA',4000000,25),
('G-306','sd 1',CONVERT(DATETIME,'01-11-2010',103),'UGANDA',4000000,28),
('G-307','rbt 1',CONVERT(DATETIME,'16-12-2016',103),'AFRICA',4800000,8),
('G-308','bd 1',CONVERT(DATETIME,'16-12-2016',103),'AFRICA',4800000,14),
('G-309','IL 1',CONVERT(DATETIME,'19-09-2014',103),'SOUTH AFRICA',4800000,11);

INSERT INTO expense(EXPENSE_ID, animal_id,FOOD_COST, MEDICINE_COST,CLEANING_COST,SERVICE_CHARGE)
VALUES('EX-02','crocodile 1',16000,9000,5000,'10%'),
('EX-03','bld 1',16500,9000,4000,'10%'),
('EX-04','bd 1',10000,6000,3000,'10%'),
('EX-05','sd 1',10000,6000,3000,'10%'),
('EX-07','hippo 1',8000,6000,2000,'10%'),
('EX-08','zebra 1',8000,6000,2000,'10%'),
('EX-09','girraf 1',10000,15000,2000,'15%'),
('EX-10','rhino 1',10000,15000,2000,'15%'),
('EX-11','zebra 1',8000,12000,2000,'15%');
 
 
 
insert into vet_details(vet_id,vet_name,staff_id,head_vet_enum,speciality,veternity_experience)
values('vet-1001', 'Anik Islam', 'S-10020', 'Yes', 'Mammale', 17),
('vet-1002', 'Toriqul Islam', 'S-10021', 'Yes', 'Reptile', 19),
('vet-1003', 'Mirazul Islam', 'S-10022', 'Yes', 'Aves', 15),
('vet-1004', 'Mohhamod Anis', 'S-10023', 'No', 'Mammale', 8),
('vet-1005', 'Rowshan Karim', 'S-10024', 'NO', 'Reptile', 6),
('vet-1006', 'Jui Khanom', 'S-10025', 'No', 'Aves', 5);

insert into visitor_details(  visitor_id, age, ticket_type_enum, zoo_ticket_code, museum_ticket_code, ticket_price,coupon_no )
values
('V-10001', 25, 'adult', 'Z-1001', 'M-1001','20tk' ,'C-1001'),
('V-10002', 12, 'child','Z-1001', 'M-1002','15tk' ,'C-1002'),
('V-10003', 10, 'child', 'Z-1003', 'M-1003','15tk' ,'C-1003'),
('V-10004', 18, 'adult', 'Z-1004', 'M-1004','20tk' ,'C-1004'),
('V-10005', 24, 'adult',  'Z-1005', 'M-1005','20tk' ,'C-1005'),
('V-10006', 1, 'free', 'Z-1006', 'M-1006', null ,'C-1006'),
('V-10007', 2, 'free', 'Z-1007', 'M-1007', null ,'C-1007'),
('V-10008', 27, 'adult', 'Z-1008', 'M-1008','20tk' ,'C-1008'),
('V-10009', 10, 'child', 'Z-1009', 'M-1009','15tk','C-1009'),
('V-10010', 9, 'child', 'Z-10010', 'M-1010','15tk','C-1010'),
('V-10011', 9, 'child', 'Z-1011', 'M-1011','15tk','C-1011'),
('V-10012', 27, 'adult','Z-1012', 'M-1012','20tk' ,'C-1012'),
('V-10013', 5, 'child', 'Z-1013', 'M-1013','15tk','C-1013'),
('V-10014', 7, 'child', 'Z-1014', 'M-1014','15tk','C-1014'),
('V-10015', 45, 'adult', 'Z-1015', 'M-1015','20tk' ,'C-1015'),
('V-10016', 6, 'child', 'Z-1016', 'M-1016','15tk','C-1016'),
('V-10017', 24, 'adult','Z-1017', 'M-1017','20tk' ,'C-1017'),
('V-10018', 8, 'child', 'Z-1018', 'M-1018','15tk','C-1018');

insert into food_court(coupon_no ,staff_id, order_id , food_type ,  food_name , price, vat)
values
('C-1001','S-10005', 'OR-1001','Baked','Pasta','280tk' ,'15%'),
('C-1002','S-10005','OR-1002', 'Baked','Pizza','600tk' ,'15%'),
('C-1003', 'S-10005', 'OR-1003','Baked','Burger','100tk' ,'15%'),
('C-1004','S-10005', 'OR-1004','Baked','Pasta','280tk' ,'15%'),
('C-1005','S-10026', 'OR-1005', 'Cold Drink', 'Apple Juice','60tk' ,'15%'),
('C-1006','S-10026', 'OR-1006', 'Cold Drink', 'Lacci','40tk' ,'15%'),
('C-1007','S-10026',  'OR-1007', 'Pastry','Vanilla Cake','60tk','15%'),
('C-1008','S-10026', 'OR-1008','Cold Drink', 'Cold Coffe','60tk','15%'),
('C-1009','S-10027',  'OR-1009', 'Soft Drink', 'Coke','20tk','15%'),
('C-1010','S-10027','OR-1010','Main Dish','Rice','50tk','15%'),
('C-1011','S-10027', 'OR-1011','Main Dish','Vegetable Curry','75tk','15%'),
('C-1012','S-10027',  'OR-1012','Main Dish','Thai Soup','120tk','15%'),
('C-1013','S-10028',  'OR-1013','Ice Cream','Cone','60tk','15%'),
('C-1014','S-10028', 'OR-1014','Ice Cream','Chocober','30tk','15%'),
('C-1015', 'S-10028', 'OR-1015', 'Pastry','Vanilla Cake','60tk', '15%'),
('C-1016','S-10028', 'OR-1016','Cold Drink', 'Mango Smoothy','140tk','15%'),
('C-1017','S-10028', 'OR-1017','Baked','Pizza','600tk' ,'15%') ;

insert into Zoo_Museum(Museum_Id, Name, Type, Import_From, Year1)
values('M1001', 'Saw fish', 'Living', 'Bhutan',2017),
('M1002', 'Cat fish', 'Living', 'Bangladesh', 2018),
('M1003', 'Piranha', 'Living', 'Mayanmar', 2016),
('M1004', 'Octopus', 'Living', 'India', 2019),
('M1005', 'Clown fish', 'Living', 'Nepal', 2017),
('M1006', 'Sea horse', 'Non living', 'Mayanmar', 2016),
('M1007', 'Hammer head', 'Non living', 'India', 2017),
('M1008', 'Baby shark', 'Non living', 'Bhutan', 2019),
('M1009', 'Trigger fish', 'Non living', 'Bangladesh', 2018),
('M1010', 'Sponge', 'Non living', 'Bangladesh', 2017),
('M1011', 'Leopard shell', 'Other', 'Bangladesh', 2016),
('M1012', 'Deer shell', 'Other','India', 2018),
('M1013', 'Elephant skeleton', 'Other', 'Mayanmar', 2019),
('M1014', 'Dynasore skeleton', 'Other', 'Nepal', 2016),
('M1015', 'Shark Skeleton', 'Other', 'India', 2017),
('M1016', 'Snake venom', 'Other', 'India', 2017);

INSERT INTO RECORD(RECORD_ID, cage_no ,staff_id, visitor_id,Museum_Id,TYPE_OF_RECORD,DATE_RECORD_CREATED,RECORD_DETAILS)
VALUES('RC-01',9,'S-10020',NULL,NULL,'SICK',CONVERT(DATETIME,'14-03-2019',103),'BOTH THE ANIMAL GOT THE FLU AND REQUIRED VACCINE GIVEN'),
('RC-02',NULL,'S-10011','V-10008','M1016','ATTEMPT TO THEFT',CONVERT(DATETIME,'21-11-2018',103),'THE VISITOR TRIED TO STEAL KING COBRA VENOM WHICH IS EXTREMELY EXPENSIVE AND WAS CAUGHT BY THE ZOO MANAGER '),
('RC-03',11,'S-10029',NULL,NULL,'SICK',CONVERT(DATETIME,'14-03-2019',103),'ONE ANIMAL GOT THE INFECTION AND REQUIRED TREATMENT WAS GIVEN');

 create table species_count(
 scintific_name varchar(100) PRIMARY KEY,
 count1 int);

 insert into species_count (scintific_name,count1)values('Ursus Americanus',5),
 (' Panthera Leo Persica',3),
 ('Axis Axis',6),
 ('Muntiacus',4),
 ('Equus Caballus',10),
 ('Rhinocerotidae',2);

 create table death (
 animal_id varchar(100),
 scintific_name varchar(100),
 reeason varchar(100)
 );


CREATE TRIGGER decree  
ON Animal_details  
FOR INSERT  
AS
BEGIN  
  update species_count
  set species_count.count1=species_count.count1+1
  where species_count.scintific_name = new.scientific_name;
END;