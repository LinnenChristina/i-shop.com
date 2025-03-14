#### Создание таблицы

```
create table if not exists client (
id serial primary key,
name varchar(50) not null,
total_purchases decimal(8,2) not null default 0.00
);
```

####  Заполнение таблицы 

```
insert into client (id,name,total_purchases)
values
('10', 'Ivan', default);
insert into client (id,name,total_purchases)
values
('11', 'Max', '1500.00');

select * from client;
```

####   Создание таблицы с constraint на FK 
```
create table if not exists Orders(
id serial primary key,
client_id int ,
order_amount decimal (8,2) check (order_amount >=0),
constraint fk_client
	foreign key (client_id) references client(id)
	on delete restrict
	on update restrict	
);
```

####   пример  таблицы с расчетом цены 
```
price_with_discount numeric(8, 2) GENERATED ALWAYS AS ((start_price - start_price / 100 * discount)) stored

CREATE TABLE IF NOT EXISTS product (
  product_id SERIAL PRIMARY KEY,               
  product_group_id INT NOT NULL,             
  product_name VARCHAR(50) NOT NULL,           
  start_price DECIMAL(5,2) NOT NULL,          
  discount DECIMAL(5,2) DEFAULT 0.00,          
  price_with_discount DECIMAL(8,2) GENERATED ALWAYS AS (start_price - (start_price / 100 * discount)) STORED, 
  product_char_code VARCHAR(8) NOT NULL,       
  count_of_products_warehouse DECIMAL(8,3) NOT NULL, 
  create_time TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP, 
  update_time TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP, 
  CONSTRAINT fk_product_group1               
    FOREIGN KEY (product_group_id)
    REFERENCES product_group (product_group_id)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION
)
```

####   пример моей таблицы c расчетом суммы на лету и несколькими CONSTRAINT 
```
CREATE TABLE IF NOT EXISTS client_order_detail (
  row_id SERIAL PRIMARY KEY,                
  client_cart_id INT NOT NULL,              
  product_id INT NOT NULL,                  
  product_price_with_discount DECIMAL(8,2) NOT NULL,
  product_count DECIMAL(8,3) NOT NULL,     
  amount_product_sum DECIMAL(8,2) GENERATED ALWAYS AS (product_price_with_discount * product_count) STORED,
  update_time TIMESTAMP NULL,              
  create_time TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP, 
  CONSTRAINT fk_client_cart_id
    FOREIGN KEY (client_cart_id)
    REFERENCES client_order (client_cart_id)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT fk_cart_id_product_id
    FOREIGN KEY (product_id)
    REFERENCES product (product_id)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION
);
```

####   Создание представления 
```
create or replace view view_client_total_purchases AS
select c.id, c.name, c.total_purchases
from client c 
where 
c.total_purchases>0;

select * from view_client_total_purchases;
```

####   Создание мат представления 
```
create materialized view mt_view_client_total_purchases AS
select c.id, c.name, c.total_purchases
from client c 
where 
c.total_purchases>0;

select * from mt_view_client_total_purchases;
```

####  Обновление записи в таблице
```
update client
set total_purchases = 2000.00
where id = 10;
```

####   Обновление мат представления 
```
refresh materialized view mt_view_client_total_purchases;
```

####   Партиционирование 
```
create table client_order(
id int generated always as identity,
client_id int not null,
order_amount decimal (8,2),
cleint_card_status_id int not null default 3,
primary key (id, cleint_card_status_id),
foreign key (client_id) references  client (id)
) 
partition by list (cleint_card_status_id);


create table cleint_card_status_id_3
partition of client_order
for values in (3);

create table cleint_card_status_id_4
partition of client_order
for values in (4);

create table cleint_card_status_id_5
partition of client_order
for values in (5);

insert into client_order (client_id, order_amount, cleint_card_status_id)
values (1,150.00,3);

insert into client_order (client_id, order_amount, cleint_card_status_id)
values (10,150.00,4);

insert into client_order (client_id, order_amount, cleint_card_status_id)
values (11,150.00,5);


select* from client_order;

select tableoid:: regclass, *from client_order;

insert into client_order (client_id, order_amount, cleint_card_status_id)
values (3,150.00,6);


INSERT INTO client_order (client_id, order_amount, client_cart_status_id)
VALUES (3, 350.00, 10); - покажет ошибку
```

####   Создание дефолтовой партиции -туда падает все, что не подходит под выделенные партиции 
```
CREATE TABLE client_order_default
PARTITION OF client_order DEFAULT;

SELECT tableoid::regclass, * FROM client_order;
```

####   Eще пример партиции на несколько статусов (11,12,13) 
```
CREATE TABLE client_order_status_10_13 
PARTITION OF client_order FOR VALUES IN (11, 12, 13);
```
