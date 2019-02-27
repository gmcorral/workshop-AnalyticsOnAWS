CREATE EXTERNAL SCHEMA nyc_tlc FROM data catalog
DATABASE 'nyc-tlc' 
iam_role 'arn:aws:iam::884265818273:role/redshift-spectrum'

SELECT * FROM nyc_tlc.yellow limit 10;


SELECT count(*) as total_rides FROM nyc_tlc.yellow;


select 
    extract(hour from to_timestamp(tpep_pickup_datetime,'YYYY-MM-DD HH24:MI:SS')) as hour_of_day,
    count(*) number_of_rides
from 
    nyc_tlc.yellow
where 
    DATE_CMP_TIMESTAMPTZ(date('2018-01-01'), to_timestamp(tpep_pickup_datetime,'YYYY-MM-DD HH24:MI:SS')) > 0 and
    DATE_CMP_TIMESTAMPTZ(date('2017-10-30'), to_timestamp(tpep_pickup_datetime,'YYYY-MM-DD HH24:MI:SS')) < 0 and
    extract(dow from to_timestamp(tpep_pickup_datetime,'YYYY-MM-DD HH24:MI:SS')) < 6
group by 1
order by 2 desc
limit 3;


select 
    extract(hour from to_timestamp(tpep_pickup_datetime,'YYYY-MM-DD HH24:MI:SS')) as hour_of_day,
    count(*) number_of_rides
from 
    nyc_tlc.yellow
where 
    DATE_CMP_TIMESTAMPTZ(date('2018-01-01'), to_timestamp(tpep_pickup_datetime,'YYYY-MM-DD HH24:MI:SS')) > 0 and
    DATE_CMP_TIMESTAMPTZ(date('2017-10-30'), to_timestamp(tpep_pickup_datetime,'YYYY-MM-DD HH24:MI:SS')) < 0 and
    extract(dow from to_timestamp(tpep_pickup_datetime,'YYYY-MM-DD HH24:MI:SS')) > 5
group by 1
order by 2 desc
limit 3;


select 
    to_date(tpep_pickup_datetime,'YYYY-MM-DD HH24:MI:SS') as date,
    avg(total_amount) as avg_amount
from 
    nyc_tlc.yellow
where 
    DATE_CMP_TIMESTAMPTZ(date('2018-01-01'), to_timestamp(tpep_pickup_datetime,'YYYY-MM-DD HH24:MI:SS')) > 0 and
    DATE_CMP_TIMESTAMPTZ(date('2017-10-30'), to_timestamp(tpep_pickup_datetime,'YYYY-MM-DD HH24:MI:SS')) < 0
group by 1
order by 2 desc
limit 10;


-- vendors Table Definition ----------------------------------------------

CREATE TABLE vendors (
    id integer PRIMARY KEY,
    name character varying(256)
);
CREATE UNIQUE INDEX vendors_pkey ON vendors(id int4_ops);

insert into vendors values (1, 'NYC Taxi')
insert into vendors values (2, 'Manhattan Cabs')


select * from public.vendors;


select 
    v.name as vendor_name,
    avg(total_amount) as avg_amount
from 
    nyc_tlc.yellow y
inner join 
    public.vendors v 
    on v.id = y.vendorid
group by 1
order by 2 desc;
