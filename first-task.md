
```
create user allen;
create database happyUsers owner allen;
\connect happyUsers

create table students (
    id          serial primary key,
    name        varchar(40) not null,
    bday        date,
    isGoodBoy   bool
);

insert into students (name, bday, isGoodBoy) values
    ('Алиса', '1998-05-15', true),
    ('Борис', '1997-09-20', true),
    ('Валентин', '1999-02-10', false),
    ('Дмитрий', '1996-11-25', true),
    ('Ева', '2000-03-30', false),
    ('Федор', '1995-07-05', true),
    ('Галина', '1994-10-12', false),
    ('Геннадий', '1993-01-18', true),
    ('Иван', '1992-04-22', false),
    ('Жан', '1991-08-28', true);

update students
set isGoodBoy = false
where bday < '1995-01-01';

delete from students where name LIKE 'А%';

select students.name
from students
WHERE bday > '1990-12-31' and isGoodBoy=true;
```
