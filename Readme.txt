������������ ������ �5

1.	�������� ������� ������ (� ������������), ������������ ����� ���� �����������, ����������� ����� � ���������� ? 75 ����.
2.	�������� ������� ������, ������� ������� ������������ ������ ��� �������, ��������� ������� ������ ������� ��������� ���� ����� ���������.
3.	�������� ������� ������ ��� ����������� �����������, � ������� ��� �����������
4.	���������� ������ �����������, ���������� ����� ������� ������� ������������ �� �����. ������� ������� ����������� � ������� ������������.

�������:
1.	����� ����������, ������� �������� ����� ������� ������� ������������ �� �����:
select s.sp_name, s.comm, o.office from office o, sperson s
where o.of_id=s.of_id and s.comm=(select max(comm) from sperson);

2.	����� �����������, � ������� ������������ ����, ��� � ������� �����:
select sp_name, comm from sperson where
comm > (select comm from sperson where sp_name=�Albert Aidj�);


3.����� �����������, � ������� ������������ ����� ��, ��� � ����� ������:

select sp_name, comm
from sperson 
where comm = (select comm from sperson where sp_name='Rodny Djons')
and sp_name!='Rodny Djons';


1.	���������� �������, � ������ ������� ������� ������������ ����, ��� � �����:
select o.office, avg(s.comm) from office o, sperson s
where o.of_id=s.of_id
group by o.office
having avg(s.comm) > (select avg(comm) from sperson where
of_id=(select of_id from office where office=�Tokyo�));

2.	����� �����������, � ������� ������������ ����, ��� � ���� �� ������ ���������� �� �����:
�) select sp_name, comm from sperson
where comm > any(select comm from sperson where
of_id =(select of_id from office where office=�Tokyo�));

�) select sp_name, comm from sperson
where comm > (select min(comm) from sperson where
of_id =(select of_id from office where office=�Tokyo�));

3.	����� �����������, � ������� ������������ ����, ��� � �������( ����) ����������� �� �����:
�) select sp_name, comm from sperson
where comm > all(select comm from sperson where
of_id =(select of_id from office where office=�Tokyo�));

�) select sp_name, comm from sperson
where comm > (select max(comm) from sperson where
of_id =(select of_id from office where office=�Tokyo�));

4.	����� �����������, � ������� ���� ���� �� ���� �����������:
 �)select s2.sp_name, s2.sp_id from sperson s2
where exists(select s1.sp_id from sperson s1 where s1.man_id=s2.sp_id);

�) select sp_name, sp_id from sperson
where sp_id in (select man_id from sperson);

5.	����� ������, � ������� ����� ������� ������� ������� ������������.
select o.office, avg(s.comm) avg_comm
from office o join sperson s on o.of_id=s.of_id
group by o.office
having avg(s.comm) = (select max(avg(comm)) from sperson group by of_id);




