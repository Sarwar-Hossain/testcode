# testcode

select
	*
from
	supportadmin_problems
where
	requested_time::date = '2021-09-08'

update
	supportadmin_problems
set
	soft_name = 'Integrated Sales and Distribution Systems'
where
	soft_name = 'Integrated Sales & Distribution Systems';

select
	distinct on
	(csall2.phoneno) phoneno
from
	client_support_admin_login_log csall2
where
	phoneno like '%01%'
order by
	phoneno;

select
	*
from
	addusers_users au
where
	au.username not in(
	select
		username
	from
		client_support_admin_login_log csall
	group by
		username)
	or au.phoneno not in (
	select
		username
	from
		client_support_admin_login_log csall
	group by
		username)
order by
	username asc;

select
	distinct on
	(username) username
from
	addusers_users au
where
	au.username not in(
	select
		distinct on
		(username) username
	from
		client_support_admin_login_log
	where
		username like '%01%')
order by
	id asc;

\

insert
	into
	clientlogin_client_info (id,
	client_name,
	client_id)
values ('1',
'Ovi',
'123');
--DELETE FROM clientlogin_complain WHERE complain_title ='test 8';

select
	distinct aa.total,
	aa.district,
	ad.area
from
	(
	select
		count(district) as total,
		district
	from
		addusers_users
	where
		district = 'Dhaka'
	group by
		district) aa
inner join addusers_users ad on
	ad.district = aa.district

select
	au.id,
	au.username,
	au.area,
	au.district,
	as2.software_name
from
	addusers_users au
inner join addusers_softwarelist as2 on
	as2.client_id = au.client_id
where
	au.district = 'Dhaka'
	and au.area = 'Uttara' ;

select
	COUNT(*)
from
	public.supportadmin_problems
where
	public.supportadmin_problems.accepted_support_username is null
	and public.supportadmin_problems.is_pending = true
	and client_id 
in (
	select
		client_id
	from
		addusers_supportperson
	where
		supportperson = 'Babu')

select
	as2.software_name,
	au.username,
	au.area,
	au.district
from
	addusers_users au
inner join addusers_softwarelist as2 on
	au.client_id = as2.client_id
where
	as2.client_id = '2245';

select
	addusers_users.*,
	addusers_softwarelist.software_name,
	as2.supportperson
from
	addusers_users
join addusers_softwarelist 
on
	addusers_softwarelist.client_id = addusers_softwarelist.client_id
join addusers_supportperson as2 on
	as2.client_id = addusers_softwarelist.client_id ;

select
	as3.supportperson
from
	addusers_supportperson as3
union
select
	sp.accepted_support_username
from
	supportadmin_problems sp;

select
	au.username,
	au.client_name, 
	case 
		when au.client_id > '2000' then 'quantity is gratter than 2000'
		when au.client_id = '2000' then 'quantity is less than 2000'
		else 'Quantity is under 2000'
	end as Quantity_text
from
	addusers_users au;

select
	ac.cusname,
	string_agg(as2.supportperson ::text, ', ')
from
	addusers_customer ac
inner join addusers_supportperson as2 
on
	cast(ac.id as text) = as2.client_id
group by
	ac.cusname;

select
	as2.client_id,
	string_agg(as2.supportperson ::text, ',')
from
	addusers_supportperson as2
group by
	as2.client_id 

select
	count(ac.cusname),
	as2.supportperson,
	string_agg(ac.cusname ::text, ', ')
from
	addusers_supportperson as2
inner join addusers_customer ac
on
	as2.client_id = cast(ac.id as text)
group by
	as2.supportperson
order by
	as2.supportperson;

select
	as2.supportperson,
	ac.cusname
from
	addusers_supportperson as2
inner join addusers_customer ac
on
	as2.client_id = cast(ac.id as text)
order by
	as2.supportperson;

select
	count(soft_id),
	sp.soft_name
from
	supportadmin_problems sp
where
	sp.soft_name = 'Financial Accounting Solution'
group by
	sp.soft_name ;

select
	*
from
	supportadmin_problems sp
where
	sp.soft_name like 'p%'
order by
	soft_name
	--Important

select
	distinct foo.*
from
	(
	select
		upper(au.area) as area
	from
		addusers_users au
	where
		au.area is not null
	order by
		au.area) as foo;

select
	soft_name
from
	supportadmin_problems csas
where
	csas.soft_name not in 
(
	select
		sp.soft_name
	from
		client_support_admin_softwarelistall sp)
order by
	soft_name;

select
	distinct foo.*
from
	(
	select
		upper(area) as area
	from
		addusers_users
	where
		dist_id = '1'
		and district = 'Dhaka'
	order by
		area) as foo
                           
select
	foo.*
from
	(
	select
		id,
		upper(dist_name) as dist_name
	from
		addusers_district
	where
		dist_name ilike '%%%%'
		order by dist_name) as foo;

select
	distinct foo.*
from
	(
	select
		upper(area) as area
	from
		addusers_users
	where
		dist_id = '1'
		and district ilike '%%%%'
	order by
		area) as foo;

select
	au.id,
	au.client_name,
	au.area,
	au.district,
	as2.software_name
from
	addusers_users au
inner join addusers_softwarelist as2 
on
	as2.client_id = au.client_id
where
	au.area ilike '%%%%'

select
	distinct au.id,
	au.client_name,
	au.area,
	au.district,
	as2.software_name
from
	addusers_users au
inner join addusers_softwarelist as2 
on
	as2.client_id = au.client_id
where
	au.district ilike '%%Dhaka%%'
	and au.area ilike '%%Uttara%%'
order by
	au.client_name ;

select
	distinct au.client_id,
	au.client_name,
	au.area,
	au.district
from
	addusers_users au
where
	au.district ilike '%%Dhaka%%'
order by
	client_name ;

select
	soft_name
from
	supportadmin_problems csas
where
	csas.soft_name not in 
(
	select
		software_name
	from
		addusers_softwarelist)
order by
	csas.soft_name ;

select
	distinct as2.client_id,
	as2.supportperson
from
	addusers_supportperson as2
where
	as2.supportperson ilike '%%liton%%';

select
	count(client_id),
	client_id,
	username
from
	addusers_users au
where
	au.client_id 
in (
	select
		cast (id as text)
	from
		addusers_customer ac)
group by
	client_id,
	username
having
	au.username = 'Shamim hossain ';

select
	Count(client_id),
	client_id,
	username
from
	addusers_users au
where
	au.client_id in (
	select
		cast (id as text)
	from
		addusers_customer ac)
group by
	client_id,
	username
having
	au.username = 'Shamim hossain ';

select
	distinct Count(client_id),
	client_id
from
	addusers_users au
where
	exists (
	select
		*
	from
		addusers_customer ac
	where
		cast (au.client_id as INTEGER) = ac.id)
group by
	client_id;

select
	all ac.cusname
from
	addusers_customer ac
where
	true;
----------------

select
	s.itemname as itemname,
	s.rpu,
	Sum(s.sqty) as qty,
	s.itemvat,
	s.servicecharge,
	s.sdvatamount as sdamt,
	Sum(s.discountamount),
	sum(s.netamount) as totalprice
from
	sale s
where
	s.saledt between '11/01/2021' and '11/03/2021'
group by
	itemname,
	s.rpu ,
	s.itemvat,
	s.servicecharge,
	s.sdvatamount
order by
	s.itemname asc;

select
	ac.cusname,
	(case
		when ac.accountant_phone_no <> '' then ac.accountant_phone_no
		else '0'
	end)
from
	addusers_customer ac;

select
	ac.cusname,
	(
	case
		when ac.accountant_phone_no <> '' then ac.accountant_phone_no
		else '0'
	end )
from
	addusers_customer ac;

create procedure SelectAllCustomers @City nvarchar(30),
@PostalCode nvarchar(10)
as
select
	*
from
	Customers
where
	City = @City
	and PostalCode = @PostalCode
go;

select
	*
from
	addusers_customer ac
where
	exists (
	select
		*
	from
		addusers_supportperson as2
	where
		cast(ac.id as text) = as2.client_id)
	--INSERT INTO client_support_admin_sellbyname (sell_by_name)
values ('Ananta Pandit'),
('Rubel Ahmed'),
('Mohammad Arifuzzaman'),
('Muhammad Abu Naser Nahid'),
('Md. Nuruzzaman'),
('Joy Narayon Roy'),
('Abdul Motin Miah'),
('Profulla Debnath'),
('Md. Arif Rabbani'),
('Imrule Kaise Raj'),
('Ripon'),
('Sabuj Debnath'),
('Md. Zobair Sheab'),
('Sonjoy Debnath'),
('Shovan Kumar Biswas Apu'),
('Shimu Yasmin'),
('Abu Sufian Al Shifat'),
('Gokul Kumar Paul'),
('Md. Samiul Reza'),
('Admin'),
('Md.Omar Faruqe'),
('Sujan Dash'),
('Sajib Saha'),
('Uzzal'),
('Sonjoy shil'),
('Prova'),
('Dourjoy'),
('Oishe Esmet Liza');

(Ananta,
Pandit) ( Rubel,
Ahmed ) ( Arifuzzaman,
Mohammad ),
( Nahid,
Muhammad ),
( Jony,
Nuruzzaman ), 
( Joy,
Narayon Roy ),
( Motin,
Abdul Miah ),
(admin),
(Rabbani,
Arif ),
(Raj,
Imrule Kaise ),
(Ripon)
(Sabuj,
Debnath ),
(Sheab,
Zobair ),
( Sonjoy,
Debnath),
(Apu,
Shovan Kumar Biswas ),
(Shimu,
Yasmin),
(Shifat,
Abu Sufian Al ),
(Gokul,
Kumar Paul ),
( Reza,
Samiul ),
( Faruqe,
Omar ),
(Sujan,
Dash),
(Sajib,
Saha),
(Uzzal),
( Sonjoy,
shil ),
( Prova,
),
(Dourjoy),
( Liza,
Oishe Esmet )
--update client_support_admin_sellbyname 
--set sell_by_name = 'Liza, Oishe Esmet' where sell_by_name = 'Oishe Esmet Liza';


select
	*
from
	pg_timezone_names
where
	abbrev = current_setting('TIMEZONE')

show timezone;
--delete from clientlogin_complain where complain_title = 'test'

alter database postgres rename to eshop;

postgres =#
select
	*
from
	pg_timezone_names
where
	name like 'UTC';

set
TIME zone 'Asia/Dhaka';
--Software info Chart
 
select
	as2.software_name,
	count(as2.software_name) NoOfSoft
from
	addusers_users au
inner join addusers_softwarelist as2 on
	au.client_id = as2.client_id
where
	au.user_created_time between date_trunc('month', CURRENT_DATE) and CURRENT_DATE
	and au.sell_by is not null
	and au.sell_by != ''
group by
	as2.software_name
	--Sell By Chart

select
	au.sell_by,
	count(au.sell_by) NoOfSoft
from
	addusers_users au
inner join addusers_softwarelist as2 on
	au.client_id = as2.client_id
where
	au.user_created_time between date_trunc('month', CURRENT_DATE) and CURRENT_DATE
	and au.sell_by is not null
	and au.sell_by != ''
group by
	au.sell_by 

select
	*
from
	date_trunc('month', CURRENT_DATE)

select
	software_name,
	count(software_name) as noOfSale
from
	(
	select
		au.client_id,
		au.client_name ,
		ss.software_name,
		au.user_created_time
	from
		addusers_users au
	inner join (
		select
			client_id ,
			software_name
		from
			addusers_softwarelist as2
) ss on
		au.client_id = ss.client_id
	where
		au.user_created_time >= date_trunc('month', CURRENT_DATE)
) foo
group by
	software_name;

select
	software_name,
	count(software_name) as noOfSale
from
	(
	select
		au.client_id,
		client_name ,
		ss.software_name,
		au.user_created_time
	from
		addusers_users au
	inner join (
		select
			client_id ,
			software_name
		from
			addusers_softwarelist as2) ss on
		au.client_id = ss.client_id
	where
		au.user_created_time >= NOW() + interval '-30 day'

) foo
group by
	software_name;

select
	software_name,
	client_name,
	user_created_time,
	sell_by,
	count(software_name) as noOfSale
from
	(
	select
		au.client_id,
		au.client_name,
		au.sell_by,
		ss.software_name,
		au.user_created_time
	from
		addusers_users au
	inner join (
		select
			client_id ,
			software_name
		from
			addusers_softwarelist as2
) ss on
		au.client_id = ss.client_id
	where
		au.user_created_time >= date_trunc('month', CURRENT_DATE)
) foo
group by
	software_name,
	client_name,
	user_created_time,
	sell_by;
--Clients

select
	au.sell_by,
	array_to_string(array_agg(au.client_name), ', ') client_name,
	count(au.client_name) NoOfClients
from
	addusers_users au
where
	au.user_created_time 
between date_trunc('month', CURRENT_DATE) and CURRENT_DATE
	and au.sell_by is not null
	and au.sell_by != ''
group by
	au.sell_by
	--no of Software
select
	au.sell_by,
	count(au.sell_by) NoOfSoft
from
	addusers_users au
inner join addusers_softwarelist as2 on
	au.client_id = as2.client_id
where
	au.user_created_time between date_trunc('month', CURRENT_DATE) and CURRENT_DATE
	and au.sell_by is not null
	and au.sell_by != ''
group by
	au.sell_by
	--Software name

select
	au.sell_by,
	array_to_string(array_agg(as2.software_name), '<br>') software_name,
	count(as2.software_name) NoOfSoft
from
	addusers_users au
inner join addusers_softwarelist as2 on
	au.client_id = as2.client_id
where
	au.user_created_time > (CURRENT_DATE - interval '31 DAY')::DATE
	and au.sell_by is not null
	and au.sell_by != ''
group by
	au.sell_by
	-- Software Name 
select
	abc.sell_by,
	array_to_string(array_agg(abc.software_name), '<br>') as software_name,
	sum(abc.noOfSoft) as noOfSoft
from
	(
	select
		au.sell_by,
		concat( as2.software_name , ' : ' , count(as2.software_name)) as software_name,
		count(as2.software_name) as noOfSoft
	from
		addusers_users au
	inner join addusers_softwarelist as2 on
		au.client_id = as2.client_id
	where
		au.user_created_time > (CURRENT_DATE - interval '31 DAY')::DATE
			and au.sell_by is not null
			and au.sell_by != ''
		group by
			au.sell_by,
			as2.software_name
    
   ) abc
group by
	abc.sell_by


select
	count(*)
from
	supportadmin_problems sp
where
	sp.accepted_support_username = 'Rasel'
	and sp.requested_time between '2022-02-01' and '2022-02-03';

select
	count("accepted_support_username") as "total"
from
	supportadmin_problems sp
where
	sp.accepted_support_username = 'ananta'
	and
sp.requested_time between date_trunc('month', CURRENT_DATE) and CURRENT_DATE;

select
	"supportadmin_problems"."accepted_support_username",
	COUNT("supportadmin_problems"."accepted_support_username") as "total"
from
	"supportadmin_problems"
where
	requested_time between date_trunc('month', CURRENT_DATE) and CURRENT_DATE
group by
	"supportadmin_problems"."accepted_support_username";

select
	"supportadmin_problems"."accepted_support_username",
	COUNT("supportadmin_problems"."accepted_support_username") as "total"
from
	"supportadmin_problems"
where
	extract('month'
from
	"supportadmin_problems"."requested_time" at TIME zone 'UTC') = 2
group by
	"supportadmin_problems"."accepted_support_username"

select
	accepted_support_username,
	count(accepted_support_username) as total
from
	supportadmin_problems
where
	requested_time 
between date_trunc('month', CURRENT_DATE) and CURRENT_DATE
group by
	accepted_support_username
order by
	accepted_support_username;

select
	*
from
	supportadmin_problems sp
where
	accepted_support_username = 'ananta'
order by
	support_accepted_time desc 


select
	"supportadmin_problems"."accepted_support_username",
	COUNT("supportadmin_problems"."accepted_support_username") as "total"
from
	"supportadmin_problems"
where
	requested_time 
between date_trunc('month', CURRENT_DATE) and CURRENT_DATE
group by
	"supportadmin_problems"."accepted_support_username"
order by
	"supportadmin_problems"."accepted_support_username"


select
	"supportadmin_problems"."accepted_support_username",
	client_name,
	client_user_name,
	accepted_support_username,
	COUNT("supportadmin_problems"."accepted_support_username") as "total"
from
	"supportadmin_problems"
where
	requested_time 
between date_trunc('month', CURRENT_DATE) and CURRENT_DATE
	and accepted_support_username = 'Shimu'
group by
	"supportadmin_problems"."accepted_support_username",
	client_name ,
	client_name,
	client_user_name,
	accepted_support_username
order by
	"supportadmin_problems"."accepted_support_username"

select
	*
from
	supportadmin_problems sp
where
	sp.client_id = '2111'
order by
	sp.requested_time desc

'2021-02-01'
	and '2021-02-28'
	and

select
	"supportadmin_problems"."client_name",
	"supportadmin_problems"."client_id",
	COUNT("supportadmin_problems"."client_name") as "total"
from
	"supportadmin_problems"
where
	"supportadmin_problems"."requested_time" >= '2022-02-01'
group by
	"supportadmin_problems"."client_name",
	"supportadmin_problems"."client_id"

select
	"supportadmin_problems"."accepted_support_username",
	COUNT("supportadmin_problems"."accepted_support_username") as "total"
from
	"supportadmin_problems"
where
	"supportadmin_problems"."requested_time" >= '2022-02-01 00:00:00+00:00 '
group by
	"supportadmin_problems"."accepted_support_username"

select
	*
from
	supportadmin_problems sp
where
	accepted_support_username = 'Shimu'
order by
	requested_time desc

select
	*
from
	supportadmin_problems sp
where
	client_id = '2111'

Passport - 4003-000140048,
	10.02.1982

select
	*
from
	addusers_users au
where
	district = 'Chittagong'
	and area = ''
  

select
	sum(case when sp.is_done is true then 1 else 0 end) as total_done_count,
	sum(case when sp.is_pending is true then 1 else 0 end) as total_pending_count,
	SUM(case when sp.is_processing then 1 else 0 end) as total_processing_count,
	SUM(case when sp.not_accepted and sp.is_pending then 1 else 0 end) as total_not_accepted_count
from
	supportadmin_problems sp;

select
	sum(case when is_done is true then 1 else 0 end) as total
from
	supportadmin_problems sp


select
	ssu.username,
	count(sp.client_id) as total
from
	supportadmin_problems sp
inner join supportadmin_support_user ssu 
on
	sp.accepted_support_username = ssu.username
group by
	ssu.username
order by
	count(sp.client_id) desc

select
	*
from
	supportadmin_problems sp
order by
	requested_time desc


select
	distinct au.sell_by,
	au.client_name,
	as2.software_name
from
	addusers_users au
inner join addusers_softwarelist as2 
on
	au.client_id = as2.client_id
where
	au.sell_by is not null
group by
	au.client_name,
	au.sell_by,
	as2.software_name
order by
	au.sell_by


select
	au.sell_by,
	foo.software_name,
	array_to_string(array_agg(au.client_name), '<br>') client_name
from
	addusers_users au
join (
	select
		as2.client_id,
		array_to_string(array_agg(as2.software_name), '<br>') software_name
	from
		addusers_softwarelist as2
	group by
		as2.client_id) as foo
on
	foo.client_id = au.client_id
where
	au.sell_by != ''
group by
	au.sell_by,
	foo.software_name
	--Sell Infomation Table

select
	au.sell_by,
	au.client_name,
	foo.software_name,
	foo.lead_by
from
	addusers_users au
join (
	select
		as2.client_id,
		as2.software_name,
		as2.lead_by
	from
		addusers_softwarelist as2) as foo
on
	foo.client_id = au.client_id
where
	au.sell_by != ''
	and au.sell_by is not null
group by
	au.sell_by,
	au.client_name,
	foo.software_name,
	foo.lead_by
order by
	au.sell_by
	--Sell Infomation Table with sell by Name

select
	au.sell_by,
	au.client_name,
	foo.software_name,
	foo.lead_by
from
	addusers_users au
join (
	select
		as2.client_id,
		as2.software_name,
		as2.lead_by
	from
		addusers_softwarelist as2
	where
		as2.lead_by is not null) as foo
on
	foo.client_id = au.client_id
where
	au.sell_by != ''
	and au.sell_by is not null
	and au.sell_by = 'Admin'
group by
	au.sell_by,
	au.client_name,
	foo.software_name,
	foo.lead_by
order by
	au.sell_by



select
	au.sell_by,
	count(au.sell_by) NoOfSoft
from
	addusers_users au
inner join addusers_softwarelist as2 on
	au.client_id = as2.client_id
where
	au.sell_by = %s
	and au.user_created_time >=%s
	and au.user_created_time <=%s
	and au.sell_by is not null
	and au.sell_by != ''
group by
	au.sell_by

insert
	into
	client_support_admin_sellbyname (sell_by_name)
values ('Digital Marketing');

select
	*
from
	addusers_users au
where
	client_id = '2389'

select
	*
from
	addusers_customer ac
where
	id = 2389

select
	*
from
	addusers_softwarelist as2
where
	client_id = '2486'

select
	*
from
	addusers_users au
where
	client_id = '1120'
	and id = 83

select
	*
from
	client_support_admin_softwarelistall csas
order by
	soft_name;

update
	addusers_softwarelist
set
	software_id = '65'
where
	software_name = 'Financial Online Accounting Systems';

select
	*
from
	addusers_users au
where
	user_created_time>'2022-02-01'




Digital Marketing

select
	*
from
	addusers_supportperson as2
where
	client_id = '2605'

select
	*
from
	addusers_customer ac
where
	id = 2389

select
	*
from
	addusers_users au
where
	au.client_id = '2389' 

select
	*
from
	addusers_users au
where
	au.client_id = '2277' 


insert
	into
	public.customer_survey_app_category (id,
	category_name)
values ('1',
'Corporate'),
('2',
'Ordinary');

select
	*
from
	customer_survey_app_customerfeedback csac
where
	question_1 is false

select
	*
from
	customer_survey_app_customerfeedback csac
where
	csac.question_4 is true 

select
	sum(case when csac.question_6 = 'Small' then 1 else 0 end) as question_6_small_part,
	sum(case when csac.question_6 = 'Medium' then 1 else 0 end) as question_6_medium_part,
	sum(case when csac.question_6 = 'Large' then 1 else 0 end) as question_6_large_part,
	sum(case when csac.question_6 = 'Extra Large' then 1 else 0 end) as question_6_extra_large_part,
	sum(case when csac.question_6 = 'Extra Extra Large' then 1 else 0 end) as question_6_extra_extra_large_part,
	sum(case when csac.question_6 = 'Small' then 1 else 1 end) as question_6_whole
from
	customer_survey_app_customerfeedback csac;

select
	sum(case when csac.question_4 is true then 1 else 0 end) as question_4_true_part,
	sum(case when csac.question_4 is false then 1 else 0 end) as question_4_false_part,
	sum(case when csac.question_4 is false then 1 else 1 end) as question_4_whole
from
	customer_survey_app_customerfeedback csac;

select
	foo.*
from
	(
	select
		*
	from
		addusers_customer ac
	inner join addusers_supportperson as2 
on
		cast(ac.id as text) = as2.client_id
	where
		as2.client_id = '2471'
		and as2.supportperson = 'Sonjoy'
		and as2.is_billing_in_charge is true
		or as2.is_billing_in_charge is false) as foo
where
	foo.supportperson = 'Sonjoy'
	and foo.is_billing_in_charge is true
	or foo.is_billing_in_charge is false 

select
	*
from
	addusers_supportperson as2
where
	as2.client_id = '2471'

select
	*
from
	public.supportadmin_problems
where
	accepted_support_username = 'Titumir'
	and comment = 'Report Correction'
order by
	support_accepted_time desc;

select
	*
from
	supportadmin_support_user ssu
where
	ssu.username = 'Titumir'

select
	*
from
	supportadmin_problems sp
where
	sp.client_name = 'Navaran Export Import Company'
order by
	support_accepted_time desc

select
	*
from
	supportadmin_problems
where
	requested_time >= date_trunc('month', CURRENT_DATE)
	and accepted_support_username = 'Sonjoy'

select
	*
from
	addusers_users au
where
	client_name = 'Steak House Cafe & Restaurant'

select
	distinct *
from
	addusers_supportperson as2
where
	as2.supportperson = 'Shifat';

select
	*
from
	addusers_customer ac
where
	cast(ac.id as text) 
in (
	select
		as2.client_id
	from
		addusers_supportperson as2
	where
		as2.supportperson = 'Shifat')

select
	*
from
	(
	select
		*
	from
		addusers_customer ac
	where
		cast(ac.id as text) 
in (
		select
			as2.client_id
		from
			addusers_supportperson as2
		where
			as2.supportperson = 'Shifat')) as abc


select
	*
into
	#TempTable
from
	customer_survey_app_category;
--CREATE TEMP TABLE tbl AS
select
	*
from
	tb6;

begin
	drop table if exists tb6;

create temp table tb6 as
	select
	category_name
from
	customer_survey_app_category;
end;

create procedure SelectAllCustomers
as
select
	*
from
	customer_survey_app_category
go;

exec SelectAllCustomers;

select
	*
from
	addusers_customer ac,
	addusers_supportperson as2
where
	cast (ac.id as text)= as2.client_id 

select
	as2.software_name,
	as2 .software_id
from
	addusers_softwarelist as2
where
	as2.client_id in (
	select
		au.client_id
	from
		addusers_users au
	where
		au.client_id > '1266')

select
	*
from
	addusers_softwarelist as2,
	addusers_users au
where
	as2.client_id = au.client_id;

select
	username,
	email,
	phoneno,
	sum_price
from
	(
	select
		au.username,
		au.email,
		au.phoneno,
		Sum(id) as sum_price
	from
		addusers_users au
	group by
		au.username,
		au.email,
		au.phoneno
	order by
		Sum(id) desc) as abc
where
	sum_price < '2000';

select
	a.client_id,
	b.client_id
from
	(
	select
		*
	from
		addusers_softwarelist as2) as a,
	(
	select
		*
	from
		addusers_users au) as b
where
	a.client_id = b.client_id;

select
	*
from
	(
	select
		B.branchname,
		A.type,
		Avg (T.amount) as [AVG],
		Count(A.accnumber) as [COUNT]
	from
		branch B,
		account A,
		transactions T
	where
		B.branchnumber = A.branchnumber
		and A.accnumber = T.accnumber
	group by
		B.branchname,
		A.type) as T1
inner join (
	select
		B1.branchname,
		Count(A1.accnumber) as [COUNT]
	from
		account A1,
		branch B1
	where
		A1.branchnumber = B1.branchnumber
	group by
		B1.branchname
	having
		Count(A1.accnumber) > 5) as T2
               on
	T1.branchname = T2.branchname;

select
	cusname
from
	(
	select
		ac.id,
		ac.cusname,
		au.username,
		au.shopname,
		au.phoneno
	from
		addusers_customer ac
	inner join addusers_users au 
on
		cast (ac.id as text)= au.client_id;

) as abc

select
	b.rating,
	foo.*
from
	(
	select
		ac.id,
		ac.cusname,
		au.username,
		au.shopname,
		au.phoneno
	from
		addusers_customer ac,
		addusers_users au
	where
		cast (ac.id as text)= au.client_id
	order by
		au.username) as foo
inner join (
	select
		abc.*
	from
		(
		select
			sp.client_id,
			avg(cast(sp.rating as int)) as rating
		from
			supportadmin_problems sp
		where
			sp .rating is not null
			and sp.client_user_phone = '01612388485'
		group by
			sp.client_id) as abc) as b
on
	b.client_id = cast (foo.id as text)


select
	a.client_id,
	b.client_id
from
	(
	select
		ac.id,
		ac.cusname,
		au.username,
		au.shopname,
		au.phoneno
	from
		addusers_customer ac,
		addusers_users au
	where
		cast (ac.id as text)= au.client_id
	order by
		au.username) as a,
	(
	select
		abc.*
	from
		(
		select
			sp.client_id,
			avg(cast(sp.rating as int)) as rating
		from
			supportadmin_problems sp
		where
			sp .rating is not null
			and sp.client_user_phone = '01612388485'
		group by
			sp.client_id) as abc) as b
where
	a.client_id = b.client_id;
------------------

select
	cast (b.rating as text) as rating,
	b.client_user_phone,
	foo.*
from
	(
	select
		ac.id,
		ac.cusname,
		au.username,
		au.shopname,
		au.phoneno
	from
		addusers_customer ac,
		addusers_users au
	where
		cast (ac.id as text) = au.client_id
	order by
		au.username) as foo
inner join (
	select
		abc.*
	from
		(
		select
			sp.client_id,
			sp.rating,
			sp.client_user_phone
		from
			supportadmin_problems sp
		where
			sp .rating is not null) as abc) as b
               on
	b.client_id = cast (foo.id as text)
where
	foo.phoneno = b.client_user_phone
order by
	foo.username;

select
	distinct cast (b.rating as text) as rating,
	b.client_user_phone,
	foo.*
from
	(
	select
		ac.id,
		ac.cusname,
		au.username,
		au.shopname,
		au.phoneno
	from
		addusers_customer ac,
		addusers_users au
	where
		cast (ac.id as text) = au.client_id
	order by
		au.username) as foo
inner join (
	select
		sp.client_id,
		sp.rating,
		sp.client_user_phone
	from
		supportadmin_problems sp) as b
        on
	b.client_id = cast (foo.id as text)
where
	foo.phoneno = b.client_user_phone
order by
	foo.username;
--------------
       
select
	ac.id,
	ac.cusname,
	au.username,
	au.shopname,
	au.phoneno,
	cast (sp.rating as text) as rating
from
	addusers_customer ac,
	addusers_users au,
	supportadmin_problems sp
where
	cast (ac.id as text) = au.client_id
	and sp.client_user_phone = au.phoneno
	and sp.rating is not null
order by
	cast (sp.rating as text);

select
	distinct foo.cusname,
	foo.username,
	foo.shopname,
	foo.phoneno,
	cast (sp.rating as text) as rating
from
	(
	select
		ac.id,
		ac.cusname,
		au.username,
		au.shopname,
		au.phoneno
	from
		addusers_customer ac,
		addusers_users au
	where
		cast (ac.id as text) = au.client_id
	order by
		au.username) as foo
inner join supportadmin_problems sp 
     on
	sp.client_id = cast (foo.id as text)
where
	sp.client_user_phone = foo.phoneno
order by
	foo.phoneno;
--final query
   
select
	distinct foo.cusname,
	foo.username,
	foo.shopname,
	foo.phoneno,
	avg(cast(sp.rating as double precision)) as rating
from
	(
	select
		ac.id,
		ac.cusname,
		au.username,
		au.shopname,
		au.phoneno
	from
		addusers_customer ac,
		addusers_users au
	where
		cast (ac.id as text) = au.client_id
	order by
		au.username) as foo
inner join supportadmin_problems sp
               on
	sp.client_id = cast (foo.id as text)
where
	sp.client_user_phone = foo.phoneno
	and sp.rating is not null
group by
	foo.cusname,
	foo.username,
	foo.shopname,
	foo.phoneno
order by
	rating;
--------------------------
--Client Rating List
--                string_agg(sp.comment ::text, ', ') as comments

select
	distinct foo.cusname,
	foo.username,
	foo.shopname,
	foo.phoneno,
	avg(cast(sp.rating as double precision)) as rating,
	array_to_string(array_agg(sp.comment), '<br>') as comments
from
	(
	select
		ac.id,
		ac.cusname,
		au.username,
		au.shopname,
		au.phoneno
	from
		addusers_customer ac,
		addusers_users au
	where
		cast (ac.id as text) = au.client_id
	order by
		au.username) as foo
inner join supportadmin_problems sp
               on
	sp.client_id = cast (foo.id as text)
where
	sp.client_user_phone = foo.phoneno
	and sp.rating is not null
group by
	foo.cusname,
	foo.username,
	foo.shopname,
	foo.phoneno
order by
	rating;
----------------------------
--Total support

select
	sp.accepted_support_username,
	Count(*) as total,
	Sum(sp.done_time - sp.support_accepted_time) / Count(*) as avg_time
from
	supportadmin_problems sp
group by
	sp.accepted_support_username
order by
	Count(*) desc;
-- Alternative 
select
	sp.accepted_support_username,
	Count(*) as total,
	To_char(Sum(sp.done_time - sp.support_accepted_time) / Count(*),
       'DD HH24:MI:SS.MS') as avg_time,
	To_char(Sum(sp.done_time - sp.assigned_time) / Count(*),
       'DD HH24:MI:SS.MS') as a_avg_time
from
	supportadmin_problems sp
group by
	sp.accepted_support_username
order by
	Count(*) desc;
--support rate data

select
	ad.accepted_support_username,
	ad.total,
	String_agg(srr.COMMENT :: text, ', ') as comments,
	ad.cus_name,
	Avg(cast(srr.rating as DOUBLE precision)) as rating
from
	supportadmin_rating_review srr
inner join (
	select
		sp.id,
		ab.accepted_support_username,
		ab.cus_name,
		ab.total
	from
		supportadmin_problems sp
	inner join (
		select
			abc.accepted_support_username,
			Count(abc.client_id)
                                             as
                                             total,
			String_agg(ac.cusname :: text, ', '
                                             ) as
                                             cus_name
		from
			addusers_customer ac
		inner join (
			select
				*
			from
				addusers_supportperson
                                             as2
			inner join
                          (
				select
					sp.accepted_support_username,
					Count(sp.accepted_support_username) as
                                     total
				from
					supportadmin_problems sp
				group by
					sp.accepted_support_username) as
                          foo
                                     on
				foo.accepted_support_username =
                                        as2.supportperson)
                                       as abc
                                     on
			abc.client_id = cast (ac.id as text)
		group by
			abc.accepted_support_username)
                                     as ab
                                  on
		sp.accepted_support_username =
                                     ab.accepted_support_username) as ad
               on
	srr.problem_id = cast (ad.id as text)
group by
	ad.accepted_support_username,
	ad.total,
	ad.cus_name;
-------------------------
         
select
	*
from
	supportadmin_problems sp
where
	sp.accepted_support_username = 'Arifuzzaman'
order by
	sp.accepted_support_username 


update
	supportadmin_problems
set
	accepted_support_username = 'kuoshik'
where
	accepted_support_username = 'Kuoshik';

select
	*
from
	addusers_customer ac

create view demo_view as 
select
	ac.cusname,
	as2.software_name
from
	addusers_customer ac,
	addusers_softwarelist as2
where
	cast (ac.id as text)= as2.client_id;

drop view demo_view;

select
	*
from
	demo_view
	--create temp table
create temporary table SALESSUMMARY (
   product_name VARCHAR(50) not null
   ,
	total_sales DECIMAL(12,
	2) not null default 0.00
   ,
	avg_unit_price DECIMAL(7,
	2) not null default 0.00
   ,
	total_units_sold INT not null default 0
);
--insert data on temp table
insert
	into
	SALESSUMMARY
   (product_name,
	total_sales,
	avg_unit_price,
	total_units_sold)
values ('cucumber',
100.25,
90,
2);
--select data from temp table
select
	*
from
	SALESSUMMARY;
--drop temp table
drop table SALESSUMMARY;
--concat value
select
	concat(ac.id, ' ---- ', ac.accountant_phone_no)
from
	addusers_customer ac
where
	ac.accountant_phone_no != '';
-- CREATE INDEX
create index demo_index on
customer_survey_app_shopuser (id)


select
	*
from
	customer_survey_app_shopuser csas;
-- Create Table
create table foo (fooid INT,
foosubid INT,
fooname text);
-- Insert Value
insert
	into
	foo
values (1,
2,
'three');

insert
	into
	foo
values (4,
5,
'six');
-- Create Function
create or replace
function get_all_foo() returns setof foo as
$BODY$
declare
    r foo%rowtype;

begin
    for r in
        select
	*
from
	foo
where
	fooid > 0
    loop
	-- can do some processing here
        return next r;
-- return current row of SELECT
end loop;

return;
end;

$BODY$
language plpgsql;
-- select data
select
	*
from
	get_all_foo();
-- Create Function
create or replace
function totalRecords ()
returns integer as $total$
declare
	total integer;

begin
   select
	count(*)
into
	total
from
	customer_survey_app_shopuser;

return total;
end;

$total$ language plpgsql;
-- select function 
select
	totalRecords ();
--parameter pass in function
create or replace
function get_sum(
    a numeric, 
    b numeric) 
returns numeric as $$
begin
    return a + b;
end;

$$
language plpgsql;
-- select function 
select
	get_sum (10,
	20);

create or replace
function GetEmployeeById(EmpId INT)  
returns customer_survey_app_shopuser  
language sql   
as   
$$  
    select
	*
from
	customer_survey_app_shopuser
where
	id = EmpId;

$$;

select
	GetEmployeeById (51)
	--Store Procedure
create or replace
	procedure GetEmployee  
(  
    EmpId INT,
	EmpName VARCHAR(100),
	EmpDob DATE,
	EmpCity VARCHAR(100),
	EmpDesignation VARCHAR(100),
	EmpJoiningDate DATE  
)  
language plpgsql as  
$$  
begin         
   select
	*
from
	customer_survey_app_shopuser
where
	id = EmpId;
end  
$$;

call GetEmployee (1);

select
	count(sp.client_id),
	sp.client_name
from
	supportadmin_problems sp
group by
	sp.client_name
having
	count(sp.client_id)>200
order by
	count(sp.client_id) desc;

select
	cast(ac.id as text) as client_id,
	ac.cusname,
	ac.accountant_phone_no,
	ac.sms_phone_no
from
	addusers_customer ac
where
	ac.is_active is not true;
--Home

select
	sum(case when sp.is_done is true then 1 else 0 end) as total_done,
	sum(case when sp.is_pending is true then 1 else 0 end) as total_pending,
	SUM(case when sp.is_processing then 1 else 0 end) as total_processing,
	SUM(case when sp.is_pending and not sp.not_accepted then 1 else 0 end) as total_new_request,
	SUM(case when sp.not_accepted and sp.is_pending then 1 else 0 end) as total_not_accepted,
	SUM(case when sp.is_helped is true then 1 else 0 end) as total_help_by
from
	supportadmin_problems sp;

select
	count(sp.soft_id) as total,
	sp.soft_name
from
	supportadmin_problems sp
group by
	sp.soft_name
order by
	count(sp.soft_id) desc;

select
	accepted_support_username,
	count(support_accepted_time) as total,
	avg(done_time - support_accepted_time) as avg_support_time
from
	supportadmin_problems
where
	support_accepted_time >= date_trunc('month', CURRENT_DATE)
group by
	accepted_support_username;

select
	sp.client_name,
	sp.soft_name,
	sp.p_description
from
	supportadmin_problems sp 

update
	supportadmin_problems sp
set
	sp.is_pending =
	case  
			when sp.is_pending is true
		and sp.is_processing is false
		and sp.is_done is false 
			then sp.is_pending is false
		and sp.is_processing is true
		and sp.is_done is false
		else sp.is_pending
	end
where
	sp.id = '74';

select
	*
from
	addusers_users au
where
	au.district = 'Satkhira'
	and au.dist_id != '64';

select
	*
from
	addusers_users au2
where
	district = 'Comilla'
	--update addusers_users set dist_id ='42' 
	--where district = 'Chandpur' and dist_id = '4';

insert
	into
	customer_survey_app_shopuser (id,
	user_name,
	email,
	password,
	is_user_active,
	shop_id,
	shop_name,
	mobile_no,
	created_time,
	created_by,
	updated_by)
values ('2',
'demo_user',
'demo@gmail.com',
'12345',
true,
'0',
'RISE', 
'+8801829075385',
'2022-03-09 18:40:20.882 +0600',
'Developer',
'Developer');

select
	*
from
	addusers_users au
where
	au.phoneno = ''

select
	*
from
	supportadmin_support_user ssu
order by
	username


select
	distinct supportperson
from
	addusers_supportperson as2
inner join supportadmin_support_user ssu
on
	as2.supportperson = ssu.username
order by
	supportperson;
-- assign support person
select
	sp.accepted_support_username,
	count(*) as total
from
	supportadmin_problems sp
where
	sp.accepted_support_username is not null
group by
	sp.accepted_support_username
order by
	sp.accepted_support_username


select
	*
from
	supportadmin_problems sp
order by
	requested_time desc;

select
	*
from
	supportadmin_problems sp
where
	sp.is_pending is true ;
-- Get Last month tota Count
select
	sum(case when sp.is_done is true then 1 else 0 end) as total_done,
	sum(case when sp.is_pending is true then 1 else 0 end) as total_pending,
	SUM(case when sp.is_processing then 1 else 0 end) as total_processing,
	SUM(case when sp.is_pending and not sp.not_accepted then 1 else 0 end) as total_new_request,
	SUM(case when sp.not_accepted and sp.is_pending then 1 else 0 end) as total_not_accepted,
	SUM(case when sp.is_helped is true then 1 else 0 end) as total_help_by
from
	supportadmin_problems sp
where
	sp.requested_time >= (CURRENT_DATE - interval '30 DAY')::DATE;
-- Get Last month Data
select
	*
from
	supportadmin_problems sp
where
	sp.requested_time >= (CURRENT_DATE - interval '30 DAY')::DATE;

select
	*
from
	supportadmin_problems sp
where
	requested_time::date <= '2022-05-12'
	and requested_time::date >= '2022-05-1'
order by
	requested_time desc;

select
	sp.accepted_support_username,
	count(*) as total
from
	supportadmin_support_user ssu
inner join supportadmin_problems sp 
on
	ssu.username = sp.accepted_support_username
group by
	sp.accepted_support_username
order by
	sp.accepted_support_username;

select
	*
from
	supportadmin_problems sp
where
	sp.accepted_support_username = 'Uzzal';
-----------------
select
	*
from
	supportadmin_problems sp
where
	sp.requested_time >= (CURRENT_DATE - interval '30 DAY')::DATE
order by
	sp.requested_time desc;

select
	distinct au.client_id,
	user_created_time
from
	addusers_users au
where
	user_created_time is not null
order by
	client_id;


select foo.accepted_support_username, foo.total_support
       from (select accepted_support_username, COUNT(*) as total_support
FROM supportadmin_problems
WHERE requested_time >= date_trunc('day', NOW()) - INTERVAL '30 day'
AND requested_time <=  date_trunc('day', NOW())
GROUP BY accepted_support_username) as foo;

select * from supportadmin_problems sp where sp."comment" = 'testing'

select accepted_support_username, COUNT(*) total_support, 
       string_agg(date_trunc('day', requested_time) ::text, ', ') as day
FROM supportadmin_problems
WHERE requested_time >= date_trunc('day', NOW()) - INTERVAL '30 day'
AND requested_time <=  date_trunc('day', NOW())
GROUP BY date_trunc('day', requested_time), accepted_support_username
order by date_trunc('day', requested_time)


select
	au.sell_by,
	array_to_string(array_agg(as2.software_name), ', ' ) as softwares_name,
	array_to_string(array_agg(au.client_name), ', ' ) as clients_name,
	count(au.sell_by) NoOfSoft,
from
	addusers_users au
inner join addusers_softwarelist as2 on
	au.client_id = as2.client_id
where
	au.user_created_time > (CURRENT_DATE - interval '365 DAY')::DATE
	and au.sell_by is not null
	and au.sell_by != ''
group by
	au.sell_by
order by au.sell_by;

--------------------

select
	as2.lead_by, 
	array_to_string(array_agg(as2.software_name), ', ' ) as softwares_name,
	array_to_string(array_agg(au.client_name), ', ' ) as clients_name,
	count(as2.lead_by) NoOfSoft
from
	addusers_users au
inner join addusers_softwarelist as2 on
	au.client_id = as2.client_id
where
	as2.lead_by is not null
	and as2.lead_by != ''
group by
	as2.lead_by
order by count(as2.lead_by) desc;

------------------------------

select sp.client_name from addusers_customer ac 
inner join supportadmin_problems sp 
on cast(ac.id as text)  = sp.client_id
where ac.is_active is true;

-----------------

select
	*
from
	addusers_customer
where
	cast(id as text) not in (
	select
		client_id
	from
		supportadmin_problems
	where
		requested_time >= (CURRENT_DATE - interval '365 DAY')::DATE)
order by
	cusname;

--------------------

select
	distinct client_name as cusname,
	count(id) as total
from
	supportadmin_problems sp
where
	sp.requested_time >= (CURRENT_DATE - interval '10 DAY')::DATE
group by
	client_name
order by
	count(id) desc;


select cusname from addusers_customer ac where cast(id as text) in 
(select client_id from supportadmin_problems sp 
where sp.requested_time >= (CURRENT_DATE - interval '10 DAY')::DATE
order by sp.requested_time);

---------------
select cusname, array_to_string(array_agg(upper(as2.supportperson)), ', ' ) as supportperson
from addusers_customer ac
inner join addusers_supportperson as2 on cast(ac.id as text)=as2.client_id 
where cast(ac.id as text) not in 
(select client_id from supportadmin_problems sp 
where sp.requested_time >= (CURRENT_DATE - interval '5 DAY')::DATE)
group by cusname
order by cusname;
-------------------
--last one year
select cusname, array_to_string(array_agg(as2.supportperson), ', ' ) as supportperson
from addusers_customer ac
inner join addusers_supportperson as2 on cast(ac.id as text)=as2.client_id 
where cast(ac.id as text) not in 
(select client_id from supportadmin_problems sp 
where sp.requested_time >= (CURRENT_DATE - interval '365 DAY')::DATE)
group by cusname
order by cusname;
