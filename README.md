CREATE DATABASE school;
USE school;
CREATE TABLE students;


INSERT INTO students (name, city)
-> VALUES ("Véronique", "Paris");

...

mysql> select * from students;
+----+-----------+-----------+
| id | name      | city      |
+----+-----------+-----------+
|  1 | Véronique | Paris     |
|  2 | Steeven   | Lyon      |
|  3 | Marc      | Marseille |
|  4 | Nour      | Lyon      |
|  5 | Romain    | Paris     |
|  6 | Sophie    | Paris     |
+----+-----------+-----------+


mysql> select * from languages;
+----+----------+
| id | name     |
+----+----------+
|  1 | French   |
|  2 | English  |
|  3 | German   |
|  4 | Spanish  |
|  5 | Mandarin |
+----+----------+

mysql> select * from favorites;
+----+------------------+------------+----------+
| id | class            | student_id | sport    |
+----+------------------+------------+----------+
|  1 | Maths            |          2 | Cricket  |
|  2 | Music            |          6 | Hip-Hop  |
|  3 | Arts             |          1 | Boxing   |
|  4 | Literature       |          3 | Tennis   |
|  5 | Computer science |          5 | Tennis   |
|  6 | Arts             |          4 | Baseball |
+----+------------------+------------+----------+

mysql> select * from students_languages;
+----+------------+-------------+
| id | student_id | language_id |
+----+------------+-------------+
|  1 |          1 |           1 |
|  2 |          1 |           2 |
|  3 |          2 |           1 |
|  4 |          2 |           3 |
|  5 |          3 |           1 |
|  6 |          4 |           1 |
|  7 |          4 |           2 |
|  8 |          4 |           4 |
|  9 |          4 |           5 |
| 10 |          5 |           1 |
| 11 |          5 |           5 |
| 12 |          6 |           1 |
| 13 |          6 |           2 |
| 14 |          6 |           3 |
+----+------------+-------------+





###### Rapport level 1

1. mysql> select * from students where id = 3;
+----+------+-----------+
| id | name | city      |
+----+------+-----------+
|  3 | Marc | Marseille |
+----+------+-----------+

2. mysql> select * from students where id = 6;
+----+--------+-------+
| id | name   | city  |
+----+--------+-------+
|  6 | Sophie | Paris |
+----+--------+-------+

3. mysql> select name, city from students where id = 1;
+-----------+-------+
| name      | city  |
+-----------+-------+
| Véronique | Paris |
+-----------+-------+

4. mysql> select name from students where id = 2;
+---------+
| name    |
+---------+
| Steeven |
+---------+


5. mysql> select * from students where city = "Paris";
+----+-----------+-------+
| id | name      | city  |
+----+-----------+-------+
|  1 | Véronique | Paris |
|  5 | Romain    | Paris |
|  6 | Sophie    | Paris |
+----+-----------+-------+

6. mysql> select name from students where city = "Lyon";
+---------+
| name    |
+---------+
| Steeven |
| Nour    |
+---------+

***

###### Rapport level 2

1. mysql> select students.name, students.city, favorites.class as "Class", favorites.sport as "Sport"
    -> from students
    -> inner join favorites on favorites.student_id = students.id
    -> where students.id = 5;
+--------+-------+------------------+--------+
| name   | city  | Class            | Sport  |
+--------+-------+------------------+--------+
| Romain | Paris | Computer science | Tennis |
+--------+-------+------------------+--------+


2. mysql> select students.name, favorites.sport as "favorite sport"
    -> from students
    -> inner join favorites on favorites.student_id = students.id
    -> where students.id = 4;
+------+----------------+
| name | favorite sport |
+------+----------------+
| Nour | Baseball       |
+------+----------------+

3. mysql> select students.name, favorites.class as "favorite"
    -> from students
    -> inner join favorites on favorites.student_id = students.id
    -> where students.id = 1;
+-----------+----------+
| name      | favorite |
+-----------+----------+
| Véronique | Arts     |
+-----------+----------+

4. mysql> select students.name, students.city, favorites.class
    -> from students
    -> inner join favorites on favorites.student_id = students.id
    -> where favorites.class = "Music";
+--------+-------+-------+
| name   | city  | class |
+--------+-------+-------+
| Sophie | Paris | Music |
+--------+-------+-------+

5. mysql> select students.name, students.city, favorites.sport
    -> from students
    -> inner join favorites on favorites.student_id = students.id
    -> where favorites.sport = "Tennis";
+--------+-----------+--------+
| name   | city      | sport  |
+--------+-----------+--------+
| Marc   | Marseille | Tennis |
| Romain | Paris     | Tennis |
+--------+-----------+--------+

6. mysql> select students.name, students.city, favorites.class
    -> from students
    -> inner join favorites on favorites.student_id = students.id
    -> where favorites.class = "Arts";
+-----------+-------+-------+
| name      | city  | class |
+-----------+-------+-------+
| Véronique | Paris | Arts  |
| Nour      | Lyon  | Arts  |
+-----------+-------+-------+


7. mysql> select count(*) from students where city = "Paris";
+----------+
| count(*) |
+----------+
|        3 |
+----------+


###### Rapport level 3


1. mysql> select students.name, students.city, languages.name, students_languages.language_id
    -> from students
    -> inner join students_languages on students.id = students_languages.student_id
    -> inner join languages on languages.id = students_languages.language_id
    -> where students.id = 1;
+-----------+-------+---------+-------------+
| name      | city  | name    | language_id |
+-----------+-------+---------+-------------+
| Véronique | Paris | French  |           1 |
| Véronique | Paris | English |           2 |
+-----------+-------+---------+-------------+

2. mysql> select students.name, students.city, languages.name, students_languages.language_id
    -> from students
    -> inner join students_languages on students.id = students_languages.student_id
    -> inner join languages on languages.id = students_languages.language_id
    -> where students.id = 4;
+------+------+----------+-------------+
| name | city | name     | language_id |
+------+------+----------+-------------+
| Nour | Lyon | French   |           1 |
| Nour | Lyon | English  |           2 |
| Nour | Lyon | Spanish  |           4 |
| Nour | Lyon | Mandarin |           5 |
+------+------+----------+-------------+


3. mysql> select students.name, languages.name
    -> from students
    -> inner join students_languages on students.id = students_languages.student_id
    -> inner join languages on languages.id = students_languages.language_id
    -> where students.id = 5;
+--------+----------+
| name   | name     |
+--------+----------+
| Romain | French   |
| Romain | Mandarin |
+--------+----------+


###### Rapport level 4


1. mysql> update students set name = "Philipp" where id = 4;
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> select * from students;
+----+-----------+-----------+
| id | name      | city      |
+----+-----------+-----------+
|  1 | Véronique | Paris     |
|  2 | Steeven   | Lyon      |
|  3 | Marc      | Marseille |
|  4 | Philipp   | Lyon      |
|  5 | Romain    | Paris     |
|  6 | Sophie    | Paris     |
+----+-----------+-----------+


2. mysql> update students set city = "Toulouse" where id = 1;
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> select * from students;
+----+-----------+-----------+
| id | name      | city      |
+----+-----------+-----------+
|  1 | Véronique | Toulouse  |
|  2 | Steeven   | Lyon      |
|  3 | Marc      | Marseille |
|  4 | Philipp   | Lyon      |
|  5 | Romain    | Paris     |
|  6 | Sophie    | Paris     |
+----+-----------+-----------+


3. mysql> SET FOREIGN_KEY_CHECKS=0;
Query OK, 0 rows affected (0.00 sec)

mysql> delete from students where city = "Paris";
Query OK, 2 rows affected (0.00 sec)
mysql> select * from students;
+----+-----------+-----------+
| id | name      | city      |
+----+-----------+-----------+
|  1 | Véronique | Toulouse  |
|  2 | Steeven   | Lyon      |
|  3 | Marc      | Marseille |
|  4 | Philipp   | Lyon      |
+----+-----------+-----------+


###### Rapport level 5


1. mysql> select students.name from students where name like "%e%";
+-----------+
| name      |
+-----------+
| Véronique |
| Steeven   |
+-----------+
2 rows in set (0.00 sec)


2. mysql> select students.name, favorites.sport
    -> from students
    -> inner join favorites on students.id = favorites.student_id
    -> where name like "%e%";
+-----------+---------+
| name      | sport   |
+-----------+---------+
| Véronique | Boxing  |
| Steeven   | Cricket |
+-----------+---------+

3. mysql> select students.name , students.city, favorites.class
    -> from students
    -> inner join favorites on students.id = favorites.student_id
    -> where city like "%i%";
+------+-----------+------------+
| name | city      | class      |
+------+-----------+------------+
| Marc | Marseille | Literature |
+------+-----------+------------+

