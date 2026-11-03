```sql

CREATE DATABASE test;

\c test

CREATE TABLE person (
id BIGINT,
first_name VARCHAR(50),
last_name VARCHAR(50),
gender VARCHAR(10),
date_of_birth DATE,
email VARCHAR(150)
);

CREATE TABLE person (
id BIGSERIAL NOT NULL PRIMARY KEY,
first_name VARCHAR(50) NOT NULL,
last_name VARCHAR(50) NOT NULL,
email VARCHAR(150) NOT NULL,
gender VARCHAR(7) NOT NULL,
date_of_birth DATE NOT NULL,
country_of_birth VARCHAR(50)
);

\d

\d person

INSERT INTO person
    (first_name, last_name, email, gender, date_of_birth, country_of_birth)
VALUES
    ('Sawata', 'Gore','sawata.gore27@gmail.com', 'Male', '2000-07-30', 'India');


SELECT * FROM person

SELECT first_name, gender
FROM person

SELECT first_name, gender, date_of_birth
FROM person
ORDER BY date_of_birth;

SELECT first_name, gender, date_of_birth
FROM person
ORDER BY date_of_birth DESC;

SELECT DISTINCT gender FROM person;

SELECT *
FROM person
WHERE gender = 'Male';

SELECT *
FROM person
WHERE gender = 'Male' AND first_name = 'Sawata';

SELECT *
FROM person
WHERE gender = 'Male' AND (first_name = 'Sawata' OR last_name='Wilson' );

SELECT *
FROM person
WHERE date_of_birth BETWEEN DATE '1995-01-01' AND DATE '2005-12-31';


SELECT 1 <= 1;

SELECT 1 <> 1;

SELECT * FROM person LIMIT 5;

SELECT * FROM person OFFSET 5 LIMIT 5;

SELECT *
FROM person OFFSET 5 FETCH FIRST 5 ROW ONLY;

SELECT *
FROM person
WHERE country_of_birth IN ('India', 'Japan');


SELECT *
FROM person
WHERE email LIKE '%.com';

SELECT *
FROM person
WHERE first_name LIKE 'Aa%';

SELECT *
FROM person
WHERE first_name LIKE 'Aa%';

SELECT *
FROM person
WHERE first_name LIKE '______.%';

SELECT *
FROM person
WHERE country_of_birth ILIKE 'i%';


SELECT country_of_birth, COUNT(*)
from person
GROUP BY country_of_birth;


SELECT country_of_birth, COUNT(*)
FROM person
GROUP BY country_of_birth
HAVING COUNT(*) > 1;

SELECT MAX(price) FROM car;
SELECT MIN(price) FROM car;
SELECT AVG(price) FROM car;
SELECT ROUND(AVG(price)) FROM car;
SELECT SUM(price) FROM car;
SELECT make, SUM(price) FROM car GROUP BY make;

SELECT make, price, price - (price * .10) FROM car;
SELECT make, price, ROUND(price - (price * .10),2) discounted_price FROM car;

SELECT COALESCE(null, 0, 33)
SELECT COALESCE(email , 'Email not provided') FROM person;

SELECT 10/0; -- ERROR
SELECT 10 / NULLIF(0,0); -- NULL
SELECT total_sales / NULLIF(total_customers, 0) FROM sales;


SELECT NOW(); --  2026-11-02 07:47:51.409851+05:30
SELECT NOW()::DATE; -- 2026-11-02
SELECT NOW()::TIME; --  07:47:51.409851

SELECT NOW() - INTERVAL '1 YEAR'; -- 2025-11-02 07:56:30.849778+05:30
SELECT NOW() - INTERVAL '10 YEARS'; -- 2016-11-02 07:57:13.877961+05:30
SELECT NOW() + INTERVAL '10 DAYS';

SELECT first_name, date_of_birth, AGE(NOW(), date_of_birth) AS age FROM person;

 ALTER TABLE person DROP CONSTRAINT person_pkey; -- to drop primary key
 ALTER TABLE person DROP ADD PRIMARY KEY (id); -- to add primary key

 DELETE FROM person WHERE id = 1;

ALTER TABLE person
ADD CONSTRAINT unique_email_address UNIQUE(email);

ALTER TABLE person ADD UNIQUE(email);

ALTER TABLE person
ADD CONSTRAINT gender_constraint
CHECK (gender = 'Female' OR gender = 'Male');

UPDATE person SET email = 'saw@gmail.com' WHERE id = 30;
UPDATE person SET email = 'saw@gmail.com', first_name = 'test'  WHERE id = 30;


INSERT INTO person (
    id, first_name, last_name, gender,
    email, date_of_birth, country_of_birth
)
VALUES (
    2017, 'Russ', 'Ruddock', 'Male',
    'rruddock@hhs.gov', DATE '1952-09-25', 'Norway'
)
ON CONFLICT (id) DO NOTHING;


INSERT INTO person (id, first_name, last_name, gender, email, date_of_birth, country_of_birth)
VALUES (2017, 'Russ', 'Ruddock', 'Male', 'new@email.com', DATE '1952-09-25', 'Norway')
ON CONFLICT (id)
DO UPDATE SET email = EXCLUDED.email;



```
