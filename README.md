![image](https://github.com/user-attachments/assets/05849f32-68cb-4a93-bb74-f6579cdeec66)


Таблица была преобразована в третью нормальную форму, так как все атрибуты зависят исключительно от первичного ключа и не имеют других зависимостей. Это стало возможным благодаря соблюдению условий первой нормальной формы, где все атрибуты являются атомарными, и второй нормальной формы, которая требует, чтобы все неключевые атрибуты зависели от полного составного ключа, а не от его части.

```c
create table address (
    postcode int primary key,
    state text not null,
    country text not null,
    address text not null
);

create table customers (
    customer_id int primary key,
    first_name text not null,
    last_name text not null,
    gender text not null,
    DOB timestamp,
    job_title text,
    job_industry_category text not null,
    wealth_segment text not null,
    deceased_indicator text not null,
    owns_car boolean not null,
    property_valuation int not null,
    postcode int not null,
    foreign key (postcode) references address(postcode)
);

create table products (
    product_id int primary key,
    brand text,
    product_line text,
    product_class text,
    product_size text,
    list_price float,
    standard_cost float
);

create table transactions (
    transaction_id int primary key,
    product_id int not null,
    customer_id int not null,
    transaction_date timestamp not null,
    online_order boolean,
    order_status text not null,
    foreign key (product_id) references products (product_id),
    foreign key (customer_id) references customers (customer_id)
);


INSERT INTO address (postcode, state, country, address) VALUES
('2016', 'New South Wales', 'Australia', '060 Morning Avenue');


INSERT INTO customers (customer_id, first_name, last_name, gender, DOB, job_title, job_industry_category, wealth_segment, deceased_indicator, owns_car, property_valuation, postcode) VALUES
(1, 'Laraine', 'Medendorp', 'F', '1953-10-12', 'Executive Secretary', 'Health', 'Mass Customer', 'N', 'Yes', 10, '2016');


INSERT INTO products (product_id, brand, product_line, product_class, product_size, list_price, standard_cost) VALUES
(86, 'OHM Cycles', 'Standard', 'medium', 'medium', 235.63, 125.07);

INSERT INTO transactions (transaction_id, product_id, customer_id, transaction_date, online_order, order_status) VALUES
(94, 86, 1, '2017-12-23', FALSE, 'Approved');
```
