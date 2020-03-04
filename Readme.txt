Лабораторная работа №5

1.	Напишите сложный запрос (с подзапросами), возвращающий имена всех сотрудников, продававших товар в количестве ? 75 штук.
2.	Напишите сложный запрос, который выводит наименования только тех товаров, стоимость которых меньше средней стоимости всех видов продукции.
3.	Напишите сложный запрос для определения сотрудников, у которых нет подчиненных
4.	Определите тройку сотрудников, получающих самый высокий процент комиссионных на фирме. Вывести фамилии сотрудников и процент комиссионных.

ПРИМЕРЫ:
1.	Найти сотрудника, который получает самый высокий процент комиссионных на фирме:
select s.sp_name, s.comm, o.office from office o, sperson s
where o.of_id=s.of_id and s.comm=(select max(comm) from sperson);

2.	Найти сотрудников, у которых комиссионные выше, чем у Алберта Айджа:
select sp_name, comm from sperson where
comm > (select comm from sperson where sp_name=’Albert Aidj’);


3.Найти сотрудников, у которых комиссионные такие же, как у Родни Джонса:

select sp_name, comm
from sperson 
where comm = (select comm from sperson where sp_name='Rodny Djons')
and sp_name!='Rodny Djons';


1.	Определить регионы, в котрых средний процент комиссионных выше, чем в Токио:
select o.office, avg(s.comm) from office o, sperson s
where o.of_id=s.of_id
group by o.office
having avg(s.comm) > (select avg(comm) from sperson where
of_id=(select of_id from office where office=’Tokyo’));

2.	Найти сотрудников, у которых комиссионные выше, чем у хотя бы одного сотрудника из Токио:
А) select sp_name, comm from sperson
where comm > any(select comm from sperson where
of_id =(select of_id from office where office=’Tokyo’));

Б) select sp_name, comm from sperson
where comm > (select min(comm) from sperson where
of_id =(select of_id from office where office=’Tokyo’));

3.	Найти сотрудников, у которых комиссионные выше, чем у каждого( всех) сотрудников из Токио:
А) select sp_name, comm from sperson
where comm > all(select comm from sperson where
of_id =(select of_id from office where office=’Tokyo’));

Б) select sp_name, comm from sperson
where comm > (select max(comm) from sperson where
of_id =(select of_id from office where office=’Tokyo’));

4.	Найти сотрудников, у которых есть хотя бы один подчиненный:
 А)select s2.sp_name, s2.sp_id from sperson s2
where exists(select s1.sp_id from sperson s1 where s1.man_id=s2.sp_id);

Б) select sp_name, sp_id from sperson
where sp_id in (select man_id from sperson);

5.	Найти регион, в котором самый высокий средний процент комиссионных.
select o.office, avg(s.comm) avg_comm
from office o join sperson s on o.of_id=s.of_id
group by o.office
having avg(s.comm) = (select max(avg(comm)) from sperson group by of_id);




