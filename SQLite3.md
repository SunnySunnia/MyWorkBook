>sqlite3 mydb.db  
>.quit  

* Foreign keys:  
  PRAGMA foreign_keys=ON  

 > **create table** clients(
  client_id integer not null primary key AUTOINCREMENT,
  lastname varchar(64)  not null,                             --not null meanning mentatory for input
  firstname varchar(64) not null,
  address varchar(64),
  city_state_zip varchar(64)
);  

>__create table__ doctors(
  doctor_id integer not null primary key AUTOINCREMENT,
  lastname varchar(64)  not null,
  firstname varchar(64) not null,
  specialty varchar(64)
);  

>__alter table__ doctors __add__   address varchar(64)  not null default '' ;  
>__alter table__ doctors __add__   city_state_zip varchar(64)  not null default '';  

>__create table__ appointments(
  appoint_id integer not null primary key AUTOINCREMENT,
  appt_date datetime not null,
  fk_client_id int not null,                 -- foreign key constraint
  fk_doctor_id int,                            -- foreign key constraint
  service varchar(64) not null,
  seen boolean,
  FOREIGN KEY (fk_client_id) REFERENCES clients (client_id), -- foreign key constraint
  FOREIGN KEY (fk_doctor_id) REFERENCES doctors (doctor_id) -- foreign key constraint
);   

>__create table__ bill_items(
  item_id integer not null primary key AUTOINCREMENT,    -- charge or payment
  fk_client_id int,                                -- foreign key constraint
  fk_doctor_id int,                              -- foreign key constraint
  fk_appoint_id int,                             -- foreign key constraint
  date     datetime  not null,
  amount  decimal(8,2) not null,
  FOREIGN KEY (fk_client_id) REFERENCES clients (client_id), -- foreign key constraint
  FOREIGN KEY (fk_doctor_id) REFERENCES doctors (doctor_id), -- foreign key constraint
  FOREIGN KEY (fk_appoint_id) REFERENCES appointments (appoint_id) -- constraint
);  

>.schema  
  to see what tables you have created.  

>__insert into__ clients
  (lastname,firstname,address,city_state_zip)
   values ('Lee', 'Sophia', NULL, 'Berkeley, CA, 94703');  

>__update__ clients __set__ address = '239 Parker St'  __where__ client_id = 1;  

>__insert into__ clients
  (lastname,firstname,address,city_state_zip)
   values ('Smith', 'Jame', '124 Maple St', 'Albany, CA, 94710');  

>__insert into__ clients
  (lastname,firstname,address,city_state_zip)
   values ('Bolivar', 'Jose', '2594 Post Ave', 'Berkeley, CA, 94705');  

>__select__ * __from__ clients;
  sqlite> select * from clients;  
1|Lee|Sophia|239 Parker St|Berkeley, CA, 94703  
2|Smith|Jame|124 Maple St|Albany, CA, 94710  
3|Bolivar|Jose|2594 Post Ave|Berkeley, CA, 94705  

sqlite> __select__ lastname __from__ clients __where__ client_id<3;  
Lee  
Smith  

sqlite> __select__ firstname,lastname __from__ clients __where__ client_id=3;  
Jose|Bolivar  

sqlite> __select__ *  __from__ clients __where__ client_id=3;  
3|Bolivar|Jose|2594 Post Ave|Berkeley, CA, 94705  

sqlite> __select__ * __from__ clients __where__ firstname __like__ 'So%';  
1|Lee|Sophia|239 Parker St|Berkeley, CA, 94703  

sqlite> __select__ * __from__ clients __where__ firstname like 'J%' __order by__ lastname;  
3|Bolivar|Jose|2594 Post Ave|Berkeley, CA, 94705  
2|Smith|Jame|124 Maple St|Albany, CA, 94710  


>drop table XXX;