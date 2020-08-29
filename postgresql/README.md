# PostgreSQL

--SELECT SELECT \* FROM film;

--DISTINCT SELECT DISTINCT release\_year FROM film; SELECT DISTINCT rental\_rate FROM film; SELECT DISTINCT rating FROM film;

--COUNT SELECT COUNT \(\*\) FROM payment; SELECT COUNT \(amount\) FROM payment; SELECT amount FROM payment; SELECT DISTINCT amount FROM payment; SELECT COUNT \(DISTINCT amount\) FROM payment;

--WHERE SELECT \* FROM customer WHERE first\_name = 'Jared';

SELECT COUNT \(title\) FROM film WHERE rental\_rate &gt; 4 AND replacement\_cost &gt;= 19.99 AND rating = 'R';

SELECT COUNT \(title\) FROM film WHERE rating = 'R' OR rating = 'PG-13';

SELECT \* FROM film WHERE rating != 'R';

SELECT email FROM customer WHERE first\_name = 'Nancy' AND last\_name = 'Thomas';

SELECT description FROM film WHERE title = 'Outlaw Hanky';

SELECT phone FROM address WHERE address = '259 Ipoh Drive';

--ORDER BY SELECT \* FROM customer ORDER BY first\_name DESC; --malejąco \(od Z do A\)

SELECT  _FROM customer ORDER BY first\_name ASC; --rosnąco \(od A do Z\)_ można używać bez ASC i w domyśle ORDER BY będzie rosnąco

SELECT store\_id, first\_name, last\_name FROM customer ORDER BY store\_id DESC, first\_name ASC;

--LIMIT SELECT \* FROM payment WHERE amount != 0.00 ORDER BY payment\_date DESC LIMIT 5;

SELECT \* FROM payment -- TIP do zobaczenia szybkiego jak wygląda dana tabela LIMIT 1;

--ORDER BY Challenge SELECT \* FROM payment LIMIT 1;

SELECT customer\_id FROM payment ORDER BY payment\_date ASC LIMIT 10;

SELECT COUNT \(length\) FROM film WHERE length &lt;= 50;

--BETWEEN SELECT \* FROM payment WHERE amount NOT BETWEEN 8 AND 9;

SELECT \* FROM payment WHERE payment\_date BETWEEN '2007-02-01' AND '2007-02-15'; --daty muszą być tak podawane 'YYYY-MM-DD'\)

--trzeba uważać na dni tygodnia, bo w przypadku tego nie mamy podanych żadnych dat do 14.02.2007 SELECT \* FROM payment WHERE payment\_date BETWEEN '2007-02-01' AND '2007-02-14';

--IN SELECT COUNT\(\*\) FROM payment WHERE amount IN \(0.99,1.98,1.99\); -- 0.99 OR 1.98 OR 1.99

SELECT COUNT\(\*\) FROM payment WHERE amount NOT IN \(0.99,1.98,1.99\);

SELECT \* FROM customer WHERE first\_name IN \('John','Jake','Julie'\);

--LIKE and ILIKE --LIKE - case-sensitive \(odróżnia duże i małe litery\) --ILIKE - case-insensitive \(nie odróżnia wielkich i małych liter\) -- nazwy zaczynające się od wielkiej litery A -- WHERE name LIKE 'A%' -- nazwy kończące się literą a -- WHERE name LIKE '%a' -- jakiś znak '_**' &lt;&lt; 3 niewiadome znaki -- WHERE title LIKE 'Mission Impossible**_ **' &lt;żeby sprawdzić część filmu -- WHERE value LIKE 'VERSION\#**' -- WHERE name LIKE '\_her%' -- Cheryl -- Theresa -- Sherri -- wszystkie 3 pasują :\)

SELECT FROM customer WHERE first\_name LIKE 'J%' AND last\_name LIKE 'S%';

SELECT \* FROM customer WHERE first\_name ILIKE 'j%' AND last\_name ILIKE 's%';

SELECT \* FROM customer WHERE first\_name LIKE '%er%'; --% procent może być też pustym znakiem przykładowo kończy się Imię na er

SELECT \* FROM customer WHERE first\_name LIKE '\_her%';

SELECT \* FROM customer WHERE first\_name NOT LIKE '\_her%';

SELECT \* FROM customer WHERE first\_name LIKE 'A%' AND last\_name NOT LIKE 'B%' ORDER BY last\_name;

--GENERAL CHALLENGE \(TEST\) --1. Ile transakcji było większych niż 5 dolarów? SELECT COUNT\(amount\) FROM payment WHERE amount &gt; 5;

--2. Ilu aktorów ma Imię zaczynające się na literę P SELECT COUNT\(first\_name\) FROM actor WHERE first\_name LIKE 'P%';

--3. Ile unikalntych dzielnic mają nasi klienci \(districts - dzielnice\) SELECT COUNT\(DISTINCT district\) FROM address;

--4. Retrieve the list of names for those distinct districts from the previous question. SELECT DISTINCT district FROM address;

--5. How many films have a rating of R and a replacement cost between $5 and $15? SELECT COUNT\(\*\) FROM film WHERE rating = 'R' AND replacement\_cost BETWEEN 5 AND 15;

--6. How many films have the word Truman somewhere in the title? SELECT COUNT\(title\) FROM film WHERE title LIKE '%Truman%';

### --Aggregate function--

--AVG\(\) -średnia zwracana jest jako float np. \(2.342418...\) jak użyjemy ROUND\(\) to możemy określić liczbę po przeicnku --COUNT\(\) -liczba --MAX\(\) -max wartość --MIN\(\) -min wartość --SUM\(\) -suma --Działają tylko w klasie SELECT lub HAVING

SELECT MIN\(replacement\_cost\) FROM film;

SELECT MAX\(replacement\_cost\) FROM film;

SELECT MAX\(replacement\_cost\), MIN\(replacement\_cost\) FROM film;

SELECT COUNT\(\*\) FROM film;

SELECT AVG\(replacement\_cost\) FROM film;

SELECT AVG\(replacement\_cost\) --ogromna liczba po przecinku FROM film;

SELECT ROUND\(AVG\(replacement\_cost\),2\) --zaokrąglenie do 2 miejsc po przecinku FROM film;

SELECT ROUND\(AVG\(replacement\_cost\),4\) FROM film;

SELECT SUM\(replacement\_cost\) FROM film;

### --GROUP BY--

SELECT customer\_id,SUM\(amount\) FROM payment GROUP BY customer\_id ORDER BY SUM\(amount\) DESC;

SELECT customer\_id,COUNT\(amount\) FROM payment GROUP BY customer\_id ORDER BY COUNT\(amount\) DESC;

SELECT staff\_id,customer\_id,SUM\(amount\) FROM payment GROUP BY staff\_id,customer\_id ORDER BY SUM\(amount\);

--DATE-- --zmiana daty z czasem na samą datę YYYY-MM-DD SELECT DATE\(payment\_date\),SUM\(amount\) FROM payment GROUP BY DATE\(payment\_date\) ORDER BY SUM\(amount\) DESC;

### --GROUP BY CHALLENGES--

/\*1. We have two staff members, with Staff IDs 1 and 2. We want to give a bonus to the staff member that handled the most payments. \(Most in terms of number of payments processed, not total dollar amount\).

How many payments did each staff meember handle and who gets the bonus?\*/ SELECT staff\_id,COUNT\(payment\_id\) FROM payment GROUP BY staff\_id ORDER BY COUNT\(payment\_id\) DESC;

/\*2. Corporate HQ is conducting a study on the relationship between replecement cost and a movie MPAA rating \(e.g G, PG, R, etc...\).

What is the average replacement cost per MPAA rating? Note: You may need to expand the AVG column to view correct results \*/ SELECT rating, ROUND\(AVG\(replacement\_cost\),2\) FROM film GROUP BY rating ORDER BY AVG\(replacement\_cost\) DESC;

/\*3. We are running a promotion to reward our top 5 customers with coupons.

What are the customer ids of the top 5 customers by total spend?\*/ SELECT customer\_id, SUM\(amount\) FROM payment GROUP BY customer\_id ORDER BY SUM\(amount\) DESC LIMIT 5;

### --HAVING--

--Używamy tylko do filtrowania po użyciu GROUP BY-- SELECT customer\_id, SUM\(amount\) FROM payment GROUP BY customer\_id HAVING SUM\(amount\) &gt; 100;

SELECT store\_id, COUNT\(customer\_id\) FROM customer GROUP BY store\_id;

SELECT store\_id, COUNT\(customer\_id\) FROM customer GROUP BY store\_id HAVING COUNT\(customer\_id\) &gt; 300;

--CHALLANGE HAVING-- /\*1. We are launching a platinum service for our most loyal customers. We will assign platinum status to customers that have had 40 or more transaction payments.

What customer\_ids are eligible for platinum status?\*/ SELECT customer\_id, COUNT\(payment\_id\) FROM payment GROUP BY customer\_id HAVING COUNT\(payment\_id\) &gt;= 40 ORDER BY COUNT\(payment\_id\) DESC;

/_2 What are the customer ids of customers who have spent more than $100 in payment transactions with our staff\_id member 2?_ / SELECT customer\_id, SUM\(amount\) FROM payment WHERE staff\_id =2 GROUP BY customer\_id HAVING SUM\(amount\) &gt;100 ORDER BY SUM\(amount\) DESC;

--Assessment Test1-- /_1. Return the customer IDs of customers who have spent at least $110 with the staff member who has an ID of 2._/ SELECT customer\_id, SUM\(amount\) FROM payment WHERE staff\_id = 2 GROUP BY customer\_id HAVING SUM\(amount\) &gt;110; --The answer should be customers 187 and 148.

/_2. How many films begin with the letter J?_/ SELECT COUNT\(title\) FROM film WHERE title LIKE 'J%'; -- The answer should be 20.

/_3. What customer has the highest customer ID number whose name starts with an 'E' and has an address ID lower than 500?_/

SELECT first\_name, last\_name FROM customer WHERE first\_name LIKE 'E%' AND address\_id &lt; 500 ORDER BY customer\_id DESC LIMIT 1; --The answer is Eddie Tomlin

### --JOINS--

/_INNER JOINS OUTER JOINS FULL JOINS UNIONS \(LEFT JOINS\) - pytanie miałem na rozmowie o to_ /

--AS Statement-- ----------------TYMCZASOWA zmiana nazwy kolumny do jednorazowego wyświetlania

SELECT COUNT\(\*\) AS num\_transactions FROM payment;

SELECT customer\_id, SUM\(amount\) AS tqotal\_spentotal\_spent FROM payment GROUP BY customer\_id;

SELECT customer\_id, SUM\(amount\) FROM payment GROUP BY customer\_id HAVING SUM\(amount\) &gt; 100;

SELECT customer\_id, SUM\(amount\) AS total\_spent FROM payment GROUP BY customer\_id HAVING SUM\(amount\) &gt; 100;

SELECT customer\_id, amount AS new\_name FROM payment WHERE amount &gt; 2;

### --Inner Joins-----

SELECT \* FROM payment INNER JOIN customer ON payment.customer\_id = customer.customer\_id;

--szukamy tylko klientów, którzy wykonali jakąś płatność SELECT payment\_id,payment.customer\_id,first\_name FROM payment INNER JOIN customer ON payment.customer\_id = customer.customer\_id;

### --Full Outer Joins--

--FULL OUTER JOIN --suma tabeli lewej z tabelą prawą SELECT \* FROM customer FULL OUTER JOIN payment ON customer.customer\_id = payment.customer\_id;

--szukamy w tabeli wartości null po zsumowaniu lewej z prawą -- czy dane są kompletne. Nie ma kogoś kto płacił i nie podał maila SELECT \* FROM customer FULL OUTER JOIN payment ON customer.customer\_id = payment.customer\_id WHERE customer.customer\_id IS null OR payment.payment\_id IS null;

SELECT COUNT\(DISTINCT customer\_id\) FROM payment; -- 599 unique\_id

SELECT COUNT\(DISTINCT customer\_id\) FROM customer; -- 599 unique\_id --nie koniecznie to nam mówi, że 599 i 599 wyników łączą się w jedno.

--LEFT OUTER JOIN--

### --LEFT OUTER JOIN == LEFT JOIN - można pisać dwie wersje!

--Tabela pierwsza \(LEWA\) łączy się z częścią wspólną prawej i zostaje LEWA plus dodatkowe informacje -- z prawej tabeli jako część wspólna

/_odpowiada na pytanie jakie filmy są możliwe do wypożyczenia aktualnie_/ SELECT film.film\_id,film.title,inventory\_id,store\_id FROM film LEFT JOIN inventory ON inventory.film\_id = film.film\_id;

--LEFT OUTER JOIN WHERE - Tylko lewa tabela BEZ części wspólnej i prawej tabeli

/ _odpowiadamy na pytanie jakich filmów z naszej wypożyczalni aktualnie nie można wypożyczyć bo są poza wypożyczalnią tzn są wypożyczone_/ SELECT film.film\_id,film.title,inventory\_id,store\_id FROM film LEFT JOIN inventory ON inventory.film\_id = film.film\_id WHERE inventory.film\_id IS null;

--RIGHT OUTER JOIN -- to samo co LEFT JOIN, ale odwrócona czyli prawa tabela jest brana pod uwagę

SELECT film.film\_id,film.title,inventory\_id,store\_id FROM film RIGHT JOIN inventory ON inventory.film\_id = film.film\_id;

SELECT film.film\_id, film.title, inventory\_id,store\_id FROM film RIGHT JOIN inventory ON inventory.film\_id = film.film\_id WHERE inventory.film\_id IS null;

### --UNION--

--Union łączenie dwóch tabel przykładowo zarobki firm z Q1 i Q2 /_SELECT_  FROM Sales2021\_Q1 UNION SELECT  _FROM Sales20201\_Q2_ /

### --JOIN CHALLENGES--

/ _1.California sales tax laws have changed and we need to alert our customers to this through email What are emails of the customers who live in California?_/

SELECT district, email FROM customer INNER JOIN address ON address.address\_id = customer.address\_id WHERE district = 'California';

/ _2. A cusomer walks in and is a huge fan of the actor "Nick Wahlberg" and wants to know which movie he is in. Get a list of all the movies "Nick Wahlberg" has been in._/

SELECT title, first\_name, last\_name FROM actor INNER JOIN film\_actor ON actor.actor\_id = film\_actor.actor\_id INNER JOIN film ON film\_actor.film\_id = film.film\_id WHERE first\_name = 'Nick' AND last\_name = 'Wahlberg';

### --Timestampt--

/ _TIME contains only time DATE contains only date TIMESTAMP contains date and time TIMESTAMPTZ contains date,time and timezone_ / -- dane można zawsze usunąć, lecz jak niezapisaliśmy daty a ją potrzebuje to przepadło. /\* TIMEZONE NOW TIMEOFDAY CURRENT\_TIME CURRENT\_DATE

### \*/

SHOW ALL; -- pokazanie różnych danych pgadmin

SHOW TIMEZONE; -- pokazanie strefy czasowej

SELECT NOW\(\); -- pokazuje aktualny timestamp with time zone

SELECT TIMEOFDAY\(\); -- pokazuje aktualny dzień i czas jako string + timezone

SELECT CURRENT\_TIME; -- sam aktualny czas

SELECT CURRENT\_DATE; -- aktualna data

### --EXTRACT-- \(wyciąg\)

/ _EXTRACT\(\) AGE\(\) TO\_CHAR\(\)_ /

/ _EXTRACT: 'zawiera' YEAR MONTH DAY WEEK QUARTER_ /

SELECT EXTRACT\(YEAR FROM payment\_date\) AS my\_year FROM payment;

SELECT EXTRACT\(MONTH FROM payment\_date\) AS pay\_month FROM payment;

SELECT EXTRACT\(QUARTER FROM payment\_date\) AS quarter\_year FROM payment;

SELECT AGE\(payment\_date\) FROM payment;

SELECT TO\_CHAR\(payment\_date, 'MONTH-YYYY'\) --FEBUARY-2007 FROM payment;

SELECT TO\_CHAR\(payment\_date, 'mon/dd/YYYY'\) --feb/15/2007 FROM payment;

SELECT TO\_CHAR\(payment\_date, 'MM-dd-YYYY'\) --02-15-2007 FROM payment;

SELECT TO\_CHAR\(payment\_date, 'dd-MM-YYYY'\) --15-02-2007 FROM payment;

--w dokumentacji pokazane jest co i jak można stosować -- [https://www.postgresql.org/docs/12/functions-formatting.html](https://www.postgresql.org/docs/12/functions-formatting.html)

--CHALLENGE TASKS

### --Timestamps and Extract

/_\[occur - pojawić się\] 1. During which months did payments occur? Format your answer to return back the full month name._ / SELECT DISTINCT\(TO\_CHAR\(payment\_date, 'MONTH'\)\) FROM payment;

/ _2. How many payments occurred on a Monday?_ / SELECT COUNT\(\*\) FROM payment WHERE TO\_CHAR\(payment\_date, 'DAY'\) LIKE 'MONDAY%';

--albo SELECT COUNT\(\*\) FROM payment WHERE EXTRACT\(dow FROM payment\_date\) = 1; -- =1 odpowiada poniedziałkowi =0 niedzieli, =2 wtorkowi itp itd... -- dow to skrót day of the week

--Matchematical Functions and Operators

### --[https://www.postgresql.org/docs/12/functions-math.html](https://www.postgresql.org/docs/12/functions-math.html)

SELECT ROUND\(rental\_rate/replacement\_cost,2\)\*100 AS percent\_cost FROM film;

SELECT 0.1 \* replacement\_cost AS deposit FROM film;

--STRING Functions and Operators

### --[https://www.postgresql.org/docs/12/functions-string.html](https://www.postgresql.org/docs/12/functions-string.html)

SELECT LENGTH\(first\_name\) FROM customer;

SELECT first\_name \|\| ' ' \|\| last\_name AS full\_name FROM customer; --laczenie imienia i nazwiska

SELECT UPPER\(first\_name\) \|\| ' ' \|\| LOWER\(last\_name\) AS full\_name FROM customer;

--tworzenie maila ze wzoru 1 litera imienia i nazwisko + @gmail.com --creating customer email addresses SELECT LOWER\(LEFT\(first\_name, 1\)\) \|\| LOWER\(last\_name\) \|\| '@gmail.com' AS custom\_email FROM customer;

### --SubQuery--

/ _1. How can we get a list of students who scored better than the average grade?_ /

--najpierw tworzymy subquery i tak samo jest odczytywane przez SQL SELECT title,rental\_rate FROM film WHERE rental\_rate &gt; \(SELECT AVG\(rental\_rate\) FROM film\);

SELECT film\_id, title FROM film WHERE film\_id IN \(SELECT inventory.film\_id FROM rental INNER JOIN inventory ON inventory.inventory\_id = rental.inventory\_id WHERE return\_date BETWEEN '2005-05-29' AND '2005-05-30'\) ORDER BY film\_id;

/ _We wanted to find customers who have at least one payment whose amount is greater than 11. We want to grab the first name and last name of those customers._ / SELECT first\_name,last\_name FROM customer AS c WHERE EXISTS \(SELECT \* FROM payment as p WHERE p.customer\_id = c.customer\_id AND amount &gt; 11\);

SELECT first\_name,last\_name FROM customer AS c WHERE NOT EXISTS -- roznica jako NOT EXSISTS \(SELECT \* FROM payment as p WHERE p.customer\_id = c.customer\_id AND amount &gt; 11\);

### --Selft-Join----

/\*uzywamy wtedy kiedy chcemy w jednej tabeli uzyć tej samej kolumny. Przykład \|\| emp\_id \|\| name \|\| report\_id\|\| \| 1 \| Andrew \| 3 \| \| 2 \| Bob \| 3 \| \| 3 \| Charlie \| 4 \| \| 4 \| David \| 1 \|

> > &gt; Chcemy wypisać kto komu musi wysłać raport z imienia \|\| name \|\| rep \|\| \| Andrew \| Charlie \| \| Bob \| Charlie \| \| Charlie \| David \| \| David \| Andrew \|

_Syntax SELECT tableA.col, tableB.col FROM table AS tableA JOIN table AS tableB ON tableA.some\_col = tableB.other\_col_ /

-- 1. Find all the pairs of films that have the same lenght SELECT title,length FROM film WHERE length = 117;

SELECT f1.title, f2.title, f1.length FROM film AS f1 INNER JOIN film AS f2 ON f1.film\_id != f2.film\_id AND f1.length = f2.length;

