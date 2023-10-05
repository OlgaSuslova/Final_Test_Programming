**1. Используя команду cat в терминале операционной системы Linux, создать два файла Домашние животные (заполнив файл собаками, кошками, хомяками) и Вьючные животными заполнив файл Лошадьми, верблюдами и ослы, а затем объединить их. Просмотреть содержимое созданного файла. Переименовать файл, дав ему новое имя (Друзья человека).**

olgas@olgas-VirtualBox:~/Documents/Final_Test_Programming$ cat > Домашние_животные

Собаки
Кошки
Хомяки
^C

olgas@olgas-VirtualBox:~/Documents/Final_Test_Programming$ cat > Вьючные_животные
Лошади
Верблюды
Ослы
^C

olgas@olgas-VirtualBox:~/Documents/Final_Test_Programming$ cat Домашние_животные Вьючные_животные > Животные

olgas@olgas-VirtualBox:~/Documents/Final_Test_Programming$ cat Животные

Собаки
Кошки
Хомяки
Лошади
Верблюды
Ослы

olgas@olgas-VirtualBox:~/Documents/Final_Test_Programming$  mv Животные Друзья_человека

olgas@olgas-VirtualBox:~/Documents/Final_Test_Programming$ cat Друзья_человека

Собаки
Кошки
Хомяки
Лошади
Верблюды
Ослы


**2. Создать директорию, переместить файл туда.**

olgas@olgas-VirtualBox:~/Documents/Final_Test_Programming$ mkdir Animals
olgas@olgas-VirtualBox:~/Documents/Final_Test_Programming$ mv Друзья_человека Animals/

**3. Подключить дополнительный репозиторий MySQL. Установить любой пакет из этого репозитория.**

olgas@olgas-VirtualBox:~/Documents/Final_Test_Programming/Animals$ sudo apt install mysql-server

olgas@olgas-VirtualBox:~/Documents/Final_Test_Programming/Animals$ sudo apt-get update


olgas@olgas-VirtualBox:~/Documents/Final_Test_Programming/Animals$ sudo service mysql status
● mysql.service - MySQL Community Server
     Loaded: loaded (/lib/systemd/system/mysql.service; enabled; vendor preset: enabled)
     Active: active (running) since Tue 2023-10-03 10:08:21 MSK; 1h 39min ago
   Main PID: 844 (mysqld)
     Status: "Server is operational"
      Tasks: 37 (limit: 2261)
     Memory: 180.1M
        CPU: 31.795s
     CGroup: /system.slice/mysql.service
             └─844 /usr/sbin/mysqld


**4. Установить и удалить deb-пакет с помощью dpkg.**

olgas@olgas-VirtualBox:~/Documents/Final_Test_Programming/Animals$ wget http://ftp.us.debian.org/debian/pool/main/s/sl/sl_5.02-1_amd64.deb

olgas@olgas-VirtualBox:~/Documents/Final_Test_Programming/Animals$ sudo dpkg -i sl_5.02-1_amd64.deb

olgas@olgas-VirtualBox:~/Documents/Final_Test_Programming/Animals$ sudo dpkg -r sl

**5. Выложить историю команд в терминале ubuntu**

see image screen.jpg

**6. Нарисовать диаграмму, в которой есть класс родительский класс, домашние животные и вьючные животные, в составы которых в случае домашних животных войдут классы: собаки, кошки, хомяки, а в класс вьючные животные войдут: Лошади, верблюды и ослы.**

see image diagram.jpg


**7. В подключенном MySQL репозитории создать базу данных “Друзья человека”**

DROP DATABASE IF EXISTS Друзья_человека;
CREATE DATABASE Друзья_человека;
USE Друзья_человека;


**8. Создать таблицы с иерархией из диаграммы в БД**

CREATE TABLE Родительский_класс (
  id INT PRIMARY KEY AUTO_INCREMENT,
  тип VARCHAR(50)
);


CREATE TABLE Домашние_животные (
  id INT PRIMARY KEY,
  вид VARCHAR(50),
  FOREIGN KEY (id) REFERENCES Родительский_класс(id)
);


CREATE TABLE Собаки (
  id INT PRIMARY KEY,
  имя VARCHAR(50),
  команда VARCHAR(50),
  дата_рождения DATE,
  FOREIGN KEY (id) REFERENCES Домашние_животные(id)
);


CREATE TABLE Кошки (
  id INT PRIMARY KEY,
  имя VARCHAR(50),
  команда VARCHAR(50),
  дата_рождения DATE,
  FOREIGN KEY (id) REFERENCES Домашние_животные(id)
);


CREATE TABLE Хомяки (
  id INT PRIMARY KEY,
  имя VARCHAR(50),
  команда VARCHAR(50),
  дата_рождения DATE,
  FOREIGN KEY (id) REFERENCES Домашние_животные(id)
);


CREATE TABLE Вьючные_животные (
  id INT PRIMARY KEY,
  вид VARCHAR(50),
  FOREIGN KEY (id) REFERENCES Родительский_класс(id)
);


CREATE TABLE Лошади (
  id INT PRIMARY KEY,
  имя VARCHAR(50),
  команда VARCHAR(50),
  дата_рождения DATE,
  FOREIGN KEY (id) REFERENCES Вьючные_животные(id)
);


CREATE TABLE Верблюды (
  id INT PRIMARY KEY,
  имя VARCHAR(50),
  команда VARCHAR(50),
  дата_рождения DATE,
  FOREIGN KEY (id) REFERENCES Вьючные_животные(id)
);


CREATE TABLE Ослы (
  id INT PRIMARY KEY,
  имя VARCHAR(50),
  команда VARCHAR(50),
  дата_рождения DATE,
  FOREIGN KEY (id) REFERENCES Вьючные_животные(id)
);


**9. Заполнить низкоуровневые таблицы именами(животных), командами которые они выполняют и датами рождения**

INSERT INTO Верблюды ( имя, команда, дата_рождения)
VALUES ('Макс', 'Но, пошел', '2019-09-01'),
       ('Кос', 'На месте' '2020-11-12'),
       ('Сим', 'Ждать' '2021-04-05');

INSERT INTO Кошки ( имя, команда, дата_рождения)
VALUES ('Пушок', 'Кис-кис', '2021-01-20'),
       ('Энжи', 'Давай играть', '2022-03-08');

INSERT INTO Лошади ( имя, команда, дата_рождения)
VALUES ('Дух', 'Но', '2020-01-21'),
       ('Сила', 'Бррррр', '2022-03-08');

INSERT INTO Ослы ( имя, команда, дата_рождения)
VALUES ('Разок', 'Пошёл', '2019-01-21'),
       ('Пуп', 'Стой', '2021-03-08');

INSERT INTO Собаки ( имя, команда, дата_рождения)
VALUES ('Шарик', 'Дай лапу', '2019-01-21'),
       ('Бим', 'Сидеть', '2020-03-08');

INSERT INTO Хомяки ( имя, команда, дата_рождения)
VALUES ('Пуфик', 'Кушать', '2022-01-21'),
       ('Носик', 'Отойди', '2023-03-08');


**10. Удалив из таблицы верблюдов, т.к. верблюдов решили перевезти в другой питомник на зимовку. Объединить таблицы лошади, и ослы в одну таблицу.**

TRUNCATE TABLE Верблюды;

CREATE TABLE Парнокопытные AS
SELECT * FROM Лошади
UNION
SELECT * FROM Ослы;

**11.Создать новую таблицу “молодые животные” в которую попадут все животные старше 1 года, но младше 3 лет и в отдельном столбце с точностью до месяца подсчитать возраст животных в новой таблице**

CREATE TABLE Парнокопытные AS
SELECT *, TIMESTAMPDIFF(MONTH, дата_рождения, CURDATE()) AS возраст_в_месяцах
FROM (
    SELECT 'Собаки' AS тип_животного, имя, команда, дата_рождения FROM Собаки
    UNION ALL
    SELECT 'Кошки' AS тип_животного, имя, команда, дата_рождения FROM Кошки
    UNION ALL
    SELECT 'Хомяки' AS тип_животного, имя, команда, дата_рождения FROM Хомяки
    UNION ALL
    SELECT 'Лошади' AS тип_животного, имя, команда, дата_рождения FROM Лошади
    UNION ALL
    SELECT 'Ослы' AS тип_животного, имя, команда, дата_рождения FROM Ослы
) AS животные
WHERE дата_рождения >= DATE_SUB(CURDATE(), INTERVAL 3 YEAR)
AND дата_рождения <= DATE_SUB(CURDATE(), INTERVAL 1 YEAR);

**12. Объединить все таблицы в одну, при этом сохраняя поля, указывающие на прошлую принадлежность к старым таблицам.**

CREATE TABLE Полный_состав AS
SELECT 'Собаки' AS тип_животного, имя, команда, дата_рождения FROM Собаки
UNION ALL
SELECT 'Кошки' AS тип_животного, имя, команда, дата_рождения FROM Кошки
UNION ALL
SELECT 'Хомяки' AS тип_животного, имя, команда, дата_рождения FROM Хомяки
UNION ALL
SELECT 'Лошади' AS тип_животного, имя, команда, дата_рождения FROM Лошади
UNION ALL
SELECT 'Ослы' AS тип_животного, имя, команда, дата_рождения FROM Ослы;












