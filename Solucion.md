--1 NOMBRE DE LAS TABLAS
SELECT name
  FROM sqlite_master
 where type = 'table';

 --2 ESTRUCTURA DE crime_scene_report
 SELECT sql
  FROM sqlite_master
 where name = 'crime_scene_report';

 --3 crime_scene_report
 SELECT description
 from crime_scene_report
 where date like '20180115' and type = 'murder' and city = 'SQL City';

 --4 BUSCAMOS LA PERSONA QUE VIVE EN NORTHWETERN DR
 SELECT *
 FROM person
 WHERE address_street_name = 'Northwestern Dr';

 --5 BUSCAMOS A ANNABEL
 SELECT *
 FROM person
 WHERE address_street_name = 'Franklin Ave' AND name like 'Annabel%';

 --6 ENTREVISTA ANNABEL
 SELECT *
 FROM interview
 INNER JOIN person ON person.id = interview.person_id
 WHERE address_street_name = 'Franklin Ave' AND name like 'Annabel%';

 --7 ENTREVISTA DE LA PERSONA DE NORTHWESTERN DONDE DALE MORTY SCHAPIRO
  SELECT *
 FROM interview
 INNER JOIN person ON person.id = interview.person_id
 WHERE address_street_name = 'Northwestern Dr';

-- LO MISMO USANDO SENTENCIAS ENLAZADAS
 SELECT * FROM PERSON
 INNER JOIN INTERVIEW ON PERSON.ID=INTERVIEW.PERSON.ID
 WHERE ADDRESS_NUMBER = (
   SELECT MAX(ADDRESS_NUMBER)
   FROM PERSON
   WHERE ADRESS_STREET_NAME LIKE 'NORTHWESTERN DR')

 --8 BUSCAMOS AL SOSPECHOSO EN EL GIMNASIO
 SELECT get_fit_now_member.name as nombre,
 	person.id as id_persona,
 	get_fit_now_member.id as id,
    get_fit_now_member.membership_status,
    drivers_license.plate_number as matricula
 FROM get_fit_now_member
 INNER join person on person.id = get_fit_now_member.person_id
 INNER join drivers_license on drivers_license.id = person.license_id
 WHERE get_fit_now_member.id like '48Z%' and membership_status = 'gold' and drivers_license.plate_number like '%H42W%';

 --9 COMPROBAMOS SI NUESTRO SOSPECHOSO ES EL CULPABLE
 INSERT INTO solution VALUES (1, 'Jeremy Bowers');
        SELECT value FROM solution;

--10 ENTREVISTAS AL ASESINO
SELECT *
FROM interview
where person_id = 67318;

 --11 BUSCAMOS AL JEFE
 SELECT	
 	person.name as nombre,
    drivers_license.hair_color as color_pelo,
    drivers_license.car_make as marca_coche,
    drivers_license.car_model as modelo_coche,
    facebook_event_checkin.event_name as evento
from person
INNER join drivers_license on drivers_license.id = person.license_id
INNER join facebook_event_checkin on facebook_event_checkin.person_id = person.id
WHERE drivers_license.car_make = 'Tesla'
	and drivers_license.car_model = 'Model S'
	and drivers_license.hair_color = 'red'
	and drivers_license.height BETWEEN 65 and 67;

 --12 COMPROBAMOS SI NUESTRO SOSPECHOSO ES EL CULPABLE JEFE
 INSERT INTO solution VALUES (1, 'Miranda Priestly');
        SELECT value FROM solution;