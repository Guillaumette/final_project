<h1> Князева Анна, группа 4589 </h1>

<h3><i> Итоговая работа</i></h3>

**Операционные системы и виртуализация (Linux)**

1. Использование команды cat в Linux:
- Создать два текстовых файла: "Pets"(Домашние животные) и "Pack animals"(вьючные животные), используя команду cat в терминале Linux. В первом файле перечислить собак, кошек и хомяков. Во втором — лошадей, верблюдов и ослов.
- Объединить содержимое этих двух файлов в один и просмотреть его содержимое.
- Переименовать получившийся файл в "Human Friends".

```
gui@gb-linux:~/final_project$ cat > Pets
собаки
кошки
хомяки
gui@gb-linux:~/final_project$ cat > Pack_animals
лошади
верблюды
ослы
gui@gb-linux:~/final_project$ cat Pets Pack_animals > Animals
gui@gb-linux:~/final_project$ cat Animals
собаки
кошки
хомяки
лошади
верблюды
ослы
gui@gb-linux:~/final_project$ mv Animals Human_Friends
```
2. Работа с директориями Linux:
- Создать новую директорию и переместить туда файл "Human Friends".
```
gui@gb-linux:~/final_project$ mkdir animals
gui@gb-linux:~/final_project$ mv Human_Friends animals
gui@gb-linux:~/final_project$ cd animals/
gui@gb-linux:~/final_project/animals$ ll
итого 12
drwxrwxr-x 2 gui gui 4096 дек 7 21:45 ./
drwxrwxr-x 3 gui gui 4096 дек 7 21:45  ../
-rw-rw-r-- 1 gui gui   76 дек 7 21:27 Humal_Friends
```
3. Работа с MySQL в Linux. “Установить MySQL на вашу вычислительную машину ”
- Подключить дополнительный репозиторий MySQL и установить один из пакетов из этого репозитория.

```
gui@gb-linux:~/final_project/animals$ wget https://dev.mysql.com/get/mysql-apt-config_0.8.26-1_all.deb
gui@gb-linux:~/final_project/animals$ sudo dpkg -i mysql-apt-config_0.8.26-1_all.deb
gui@gb-linux:~/final_project/animals$ sudo apt install mysql-client mysql-community-server mysql-server
gui@gb-linux:~/final_project/animals$ sudo apt update
gui@gb-linux:~/final_project/animals$ sudo mysql_secure_installation
gui@gb-linux:~/final_project/animals$ sudo mysql
```

4. Управление deb-пакетами
- Установить и затем удалить deb-пакет, используя команду dpkg.

```
gui@gb-linux:~$ apt download lftp
gui@gb-linux:~$ sudo dpkg -i lftp_4.9.2-1build1_amd64.deb
gui@gb-linux:~$ sudo dpkg -r lftp
```

5. История команд в терминале Ubuntu

```
  cat > Pets
  cat > Pack_animals
  cat Pets Pack_animals > Animals
  cat Animals 
  mv Animals Human_Friends
  ll
  mkdir animals
  mv Human_Friends animals
  ll
  cd animals/
  ll
  sudo apt install mysql-server
  wget https://dev.mysql.com/get/mysql-apt-config_0.8.26-1_all.deb
  sudo dpkg -i mysql-apt-config_0.8.26-1_all.deb
  sudo apt update
  sudo apt install mysql-client mysql-community-server mysql-server
  sudo mysql_secure_installation
  sudo mysql
  history
  apt download lftp
  sudo dpkg -i lftp_4.9.2-1build1_amd64.deb
  sudo dpkg -r lftp
  history 
```

**ООП**

6. Диаграмма классов
- Создать диаграмму классов с родительским классом "Животные", и двумя подклассами: "Pets" и "Pack animals". В составы классов которых в случае Pets войдут классы: собаки, кошки, хомяки, а в класс Pack animals войдут: Лошади, верблюды и ослы). Каждый тип животных будет характеризоваться (например, имена, даты рождения, выполняемые команды и т.д) Диаграмму можно нарисовать в любом редакторе, такими как Lucidchart, Draw.io, Microsoft Visio и других.

![Диаграмма](/img/diagram.png)

7. Работа с MySQL (Задача выполняется в случае успешного выполнения задачи “Работа с MySQL в Linux. “Установить MySQL на вашу машину”

7.1. После создания диаграммы классов в 6 пункте, в 7 пункте база данных "Human Friends" должна быть структурирована в соответствии с этой диаграммой. Например, можно создать таблицы, которые будут соответствовать классам "Pets" и "Pack animals", и в этих таблицах будут поля, которые характеризуют каждый тип животных (например, имена, даты рождения, выполняемые команды и т.д.).

7.2.

- В ранее подключенном MySQL создать базу данных с названием "Human Friends".

```
DROP DATABASE IF EXISTS human_friends;
CREATE DATABASE human_friends;
```

- Создать таблицы, соответствующие иерархии из вашей диаграммы классов.

```
USE human_friends;

CREATE TABLE animals (
	id INT AUTO_INCREMENT PRIMARY KEY, 
	class_name VARCHAR(20)
);

INSERT INTO
	animals (class_name)
VALUES 
	('Pack_animals'),
	('Pets');  

CREATE TABLE pack_animals (
	id INT AUTO_INCREMENT PRIMARY KEY,
    subclass_name VARCHAR (20),
    class_id INT,
    FOREIGN KEY (class_id) REFERENCES animals (id) ON DELETE CASCADE ON UPDATE CASCADE
);

INSERT INTO 
	pack_animals (subclass_name, class_id)
VALUES
	('Horses', 1),
	('Donkeys', 1),  
	('Camels', 1); 
    
CREATE TABLE pets (
	id INT AUTO_INCREMENT PRIMARY KEY,
    subclass_name VARCHAR (20),
    class_id INT,
    FOREIGN KEY (class_id) REFERENCES animals (id) ON DELETE CASCADE ON UPDATE CASCADE
);

INSERT INTO 
	pets (subclass_name, class_id)
VALUES 
	('Cats', 2),
	('Dogs', 2),  
	('Hamsters', 2); 

CREATE TABLE cats (       
    id INT AUTO_INCREMENT PRIMARY KEY, 
    name VARCHAR(20), 
    type_id INT, 
    birthday DATE,
    commands VARCHAR(50),
    Foreign KEY (type_id) REFERENCES pets (id) ON DELETE CASCADE ON UPDATE CASCADE
);

CREATE TABLE dogs (       
    id INT AUTO_INCREMENT PRIMARY KEY, 
    name VARCHAR(20), 
    type_id INT, 
    birthday DATE,
    commands VARCHAR(50),
    Foreign KEY (type_id) REFERENCES pets (id) ON DELETE CASCADE ON UPDATE CASCADE
);

CREATE TABLE hamsters (       
    id INT AUTO_INCREMENT PRIMARY KEY, 
    name VARCHAR(20), 
    type_id INT, 
    birthday DATE,
    commands VARCHAR(50),
    Foreign KEY (type_id) REFERENCES pets (id) ON DELETE CASCADE ON UPDATE CASCADE
);

CREATE TABLE horses (       
    id INT AUTO_INCREMENT PRIMARY KEY, 
    name VARCHAR(20), 
    type_id INT, 
    birthday DATE,
    commands VARCHAR(50),
    Foreign KEY (type_id) REFERENCES pack_animals (id) ON DELETE CASCADE ON UPDATE CASCADE
);

CREATE TABLE donkeys (       
    id INT AUTO_INCREMENT PRIMARY KEY, 
    name VARCHAR(20), 
    type_id INT, 
    birthday DATE,
    commands VARCHAR(50),
    Foreign KEY (type_id) REFERENCES pack_animals (id) ON DELETE CASCADE ON UPDATE CASCADE
);

CREATE TABLE camels (       
    id INT AUTO_INCREMENT PRIMARY KEY, 
    name VARCHAR(20), 
    type_id INT, 
    birthday DATE,
    commands VARCHAR(50),
    Foreign KEY (type_id) REFERENCES pack_animals (id) ON DELETE CASCADE ON UPDATE CASCADE
);
```

- Заполнить таблицы данными о животных, их командах и датами рождения.

```
INSERT INTO 
	cats (name, type_id, birthday, commands)
VALUES 
	('Murzik', 1, '2020-09-10', 'Sit, Pounce'),
	('Barsik', 1, '2019-01-21', 'Sit, Pounce, Scratch'),  
	('Tractor', 1, '2021-07-13', 'Meow, Scratch, Jump'); 

INSERT INTO 
	dogs (name, type_id, birthday, commands)
VALUES 
	('Sharik', 2, '2015-09-10', 'Sit, Stay, Fetch'),
	('Bobik', 2, '2020-06-13', 'Sit, Paw, Bark'),  
	('Barbos', 2, '2018-01-26', 'Sit, Stay, Roll'); 

INSERT INTO 
	hamsters (name, type_id, birthday, commands)
VALUES 
	('Spotty', 3, '2021-03-10', 'Roll, Hide'),
	('Coconut', 3, '2021-08-01', 'Roll, Spin'); 

INSERT INTO 
	horses (name, type_id, birthday, commands)
VALUES 
	('Vibriss', 1, '2020-09-10', 'Trot, Canter, Gallop'),
	('Thunder', 1, '2010-01-27', 'Trot, Canter'),  
	('Blust', 1, '2018-10-03', 'Trot, Jump, Gallop'); 

INSERT INTO 
	donkeys (name, type_id, birthday, commands)
VALUES 
	('Dragonlover', 2, '2017-09-18', 'Walk, Carry Load, Bray'), 
	('Ia', 2, '2019-01-23', 'Walk, Bray, Kick'); 

INSERT INTO 
	camels (name, type_id, birthday, commands)
VALUES 
	('Patrick', 3, '2016-11-03', 'Walk, Carry Load'),
	('TimothyShalame', 3, '2018-12-12', 'Walk, Sit'), 
	('Desert', 3, '2015-08-14', 'Walk, Run'); 
```

- Удалить записи о верблюдах и объединить таблицы лошадей и ослов.

```
DELETE FROM camels;

CREATE TABLE horses_and_donkeys 
SELECT * FROM horses
	UNION 
SELECT * FROM donkeys;
```

- Создать новую таблицу для животных в возрасте от 1 до 3 лет и вычислить их возраст с точностью до месяца.

```
DROP TABLE IF EXISTS temp_animals;
CREATE TEMPORARY TABLE temp_animals AS
SELECT * FROM cats
UNION
SELECT * FROM dogs
UNION
SELECT * FROM hamsters
UNION
SELECT * FROM horses
UNION
SELECT * FROM donkeys
UNION
SELECT * FROM camels;

DROP TABLE IF EXISTS young_animals;
CREATE TABLE young_animals
SELECT
	name, type_id, birthday, commands, TIMESTAMPDIFF(MONTH, birthday, CURDATE()) AS age_in_month
FROM 
	temp_animals
WHERE birthday BETWEEN ADDDATE(CURDATE(), INTERVAL -3 YEAR) AND ADDDATE(CURDATE(), INTERVAL -1 YEAR);
```

- Объединить все созданные таблицы в одну, сохраняя информацию о принадлежности к исходным таблицам.

```
DROP TABLE IF EXISTS all_animals;
CREATE TABLE all_animals

SELECT 
	dg.name,
	p.subclass_name, 
	dg.birthday, 
	dg.commands,
	a.class_name
FROM dogs dg
LEFT JOIN pets p ON p.id = dg.type_id
LEFT JOIN animals a ON a.id = p.class_id
UNION
SELECT 
	ct.name,
	p.subclass_name, 
	ct.birthday, 
	ct.commands,
	a.class_name
FROM cats ct
LEFT JOIN pets p ON p.id = ct.type_id
LEFT JOIN animals a ON a.id = p.class_id
UNION
SELECT 
	hm.name,
	p.subclass_name, 
	hm.birthday, 
	hm.commands,
	a.class_name
FROM hamsters hm
LEFT JOIN pets p ON p.id = hm.type_id
LEFT JOIN animals a ON a.id = p.class_id
UNION
SELECT 
	hr.name,
	pa.subclass_name, 
	hr.birthday, 
	hr.commands,
	a.class_name
FROM horses hr
LEFT JOIN pack_animals pa ON pa.id = hr.type_id
LEFT JOIN animals a ON a.id = pa.class_id
UNION
SELECT 
	dk.name,
	pa.subclass_name, 
	dk.birthday, 
	dk.commands,
	a.class_name
FROM donkeys dk
LEFT JOIN pack_animals pa ON pa.id = dk.type_id
LEFT JOIN animals a ON a.id = pa.class_id
UNION
SELECT 
	cm.name,
	pa.subclass_name, 
	cm.birthday, 
	cm.commands,
	a.class_name
FROM camels cm
LEFT JOIN pack_animals pa ON pa.id = cm.type_id
LEFT JOIN animals a ON a.id = pa.class_id
```

8. ООП и Java

- Создать иерархию классов в Java, который будет повторять диаграмму классов созданную в задаче 6 (Диаграмма классов).

9. Программа-реестр домашних животных

Написать программу на Java, которая будет имитировать реестр домашних животных. Должен быть реализован следующий функционал:
9.1. Добавление нового животного - Реализовать функциональность для добавления новых животных в реестр. Животное должно определяться в правильный класс (например, "собака", "кошка", "хомяк" и т.д.)

9.2. Список команд животного - Вывести список команд, которые может выполнять добавленное животное (например, "сидеть", "лежать").

9.3. Обучение новым командам - Добавить возможность обучать животных новым командам.

9.4. Вывести список животных по дате рождения

9.5. Навигация по меню - Реализовать консольный пользовательский интерфейс с меню для навигации между вышеуказанными функциями.

10. Счетчик животных Создать механизм, который позволяет вывести на экран общее количество созданных животных любого типа (Как домашних, так и вьючных), то есть при создании каждого нового животного счетчик увеличивается на “1”.
