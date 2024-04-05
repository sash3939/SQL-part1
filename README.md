# Домашнее задание к занятию «SQL. Часть 1»

---

Задание можно выполнить как в любом IDE, так и в командной строке.

### Задание 1

Получите уникальные названия районов из таблицы с адресами, которые начинаются на “K” и заканчиваются на “a” и не содержат пробелов.

### Решение 1
[address](https://github.com/sash3939/SQL-part1/assets/156709540/d563e2e3-cb5e-4bbd-be57-d63a66bf8ec8)

SELECT DISTINCT district
FROM sakila.address
WHERE district LIKE 'K%a' AND 'district' NOT LIKE '% %';

---

### Задание 2

Получите из таблицы платежей за прокат фильмов информацию по платежам, которые выполнялись в промежуток с 15 июня 2005 года по 18 июня 2005 года **включительно** и стоимость которых превышает 10.00.

### Решение 2
[payment](https://github.com/sash3939/SQL-part1/assets/156709540/a0da3977-6a7f-4ceb-b07f-30b02f42e0b9)


SELECT *
FROM sakila.payment
WHERE payment_date BETWEEN '2005-06-15' AND '2005-06-18 23:59:59'
AND amount > 10.00;

---

### Задание 3

Получите последние пять аренд фильмов.

### Решение 3
[rental](https://github.com/sash3939/SQL-part1/assets/156709540/1f07b7ec-9320-4902-870c-e6515749b8a2)

SELECT *
FROM sakila.rental ORDER BY rental_date DESC
LIMIT 5;

---

### Задание 4

Одним запросом получите активных покупателей, имена которых Kelly или Willie. 

Сформируйте вывод в результат таким образом:
- все буквы в фамилии и имени из верхнего регистра переведите в нижний регистр,
- замените буквы 'll' в именах на 'pp'.

### Решение 4
[replace](https://github.com/sash3939/SQL-part1/assets/156709540/19ba57ff-23c5-4f78-ab02-a7e5f32e6035)

SELECT 
    replace(lower(first_name), 'll', 'pp') AS modified_name
FROM 
    sakila.customer
WHERE 
    first_name IN ('Kelly', 'Willie');

---    
## Дополнительные задания (со звёздочкой*)
Эти задания дополнительные, то есть не обязательные к выполнению, и никак не повлияют на получение вами зачёта по этому домашнему заданию. Вы можете их выполнить, если хотите глубже шире разобраться в материале.

### Задание 5*

Выведите Email каждого покупателя, разделив значение Email на две отдельных колонки: в первой колонке должно быть значение, указанное до @, во второй — значение, указанное после @.

### Решение 5*
[email](https://github.com/sash3939/SQL-part1/assets/156709540/19c3582c-ca77-4422-b9a6-71270aec4ff3)

SELECT 
    SUBSTRING_INDEX(email, '@', 1) AS name,
    SUBSTRING_INDEX(email, '@', -1) AS domain
FROM 
    sakila.customer

---

### Задание 6*

Доработайте запрос из предыдущего задания, скорректируйте значения в новых колонках: первая буква должна быть заглавной, остальные — строчными.

### Решение 6*
[concat](https://github.com/sash3939/SQL-part1/assets/156709540/b6136d2f-a0ac-4669-beb3-3a5c201c563e)


SELECT 
    CONCAT(
        UPPER(SUBSTRING(SUBSTRING_INDEX(email, '@', 1), 1, 1)),
        LOWER(SUBSTRING(SUBSTRING_INDEX(email, '@', 1), 2))
    ) AS username,
    LOWER(SUBSTRING_INDEX(email, '@', -1)) AS domain
FROM 
    sakila.customer
