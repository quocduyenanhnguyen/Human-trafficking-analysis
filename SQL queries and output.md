### 1. Number of global victims by data source
```
SELECT distinct Datasource, count(Datasource) as datasource_count FROM global_trafficking_data
group by Datasource
order by datasource_count desc
;
```
#### Output
![Screen Shot 2024-06-30 at 10 27 48 PM](https://github.com/quocduyenanhnguyen/Human-trafficking-analysis/assets/92205707/af2dd943-836a-4f12-9667-c93caa2381a4)

-> most victims received services from hotline (i.e. remote means of communication such as email, phone call, online form report, text message, etc)

### 2. Number of victims by year of registration for assistance from IOM
```
SELECT distinct yearOfRegistration, count(Datasource) as yearOfRegistration_count FROM global_trafficking_data
group by yearOfRegistration
order by yearOfRegistration_count desc
;
```
#### Output
![Screen Shot 2024-06-30 at 10 28 38 PM](https://github.com/quocduyenanhnguyen/Human-trafficking-analysis/assets/92205707/fb7d79ec-2f72-4d73-a265-0e09a3f86e1d)

-> most victims registered in the year 2019. 

### 3. Gender of victims
```
SELECT distinct gender, count(Datasource) as gender_count FROM global_trafficking_data
group by gender
order by gender_count desc
;
```
#### Output
![Screen Shot 2024-06-30 at 10 29 19 PM](https://github.com/quocduyenanhnguyen/Human-trafficking-analysis/assets/92205707/3abb9c8a-c373-4ac3-b915-8d59f476c469)

-> most victims are females

### 4. Where most victims located?
```
SELECT distinct r.Country, count(Datasource) as citizenship_count FROM global_trafficking_data gd
left join region r on r.iso2 = gd.citizenship
group by r.Country
order by citizenship_count desc
;
```
#### Output
![Screen Shot 2024-06-30 at 10 30 14 PM](https://github.com/quocduyenanhnguyen/Human-trafficking-analysis/assets/92205707/f721a395-1567-45dd-be97-291640ec2c84)

-> there are quite a few missing data. If we don't count missing data, Philippines has the most victims registered with IOM.

### 5. Number of victims of forced labor by year of registration
```
SELECT distinct yearOfRegistration, count(Datasource) as forced_labor_count FROM global_trafficking_data gd
where isForcedLabour = 1
group by yearOfRegistration
order by forced_labor_count desc
;
```
#### Output
![Screen Shot 2024-06-30 at 10 31 22 PM](https://github.com/quocduyenanhnguyen/Human-trafficking-analysis/assets/92205707/21c7139b-1723-4111-8e49-a4a1a0f9874b)

-> most victims of forced labor registered in year 2019. 

### 6. Number of victims of sexual exploitation by year of registration
```
SELECT distinct yearOfRegistration, count(Datasource) as SexualExploit_count FROM global_trafficking_data gd
where isSexualExploit = 1
group by yearOfRegistration
order by SexualExploit_count desc
;
```
#### Output
![Screen Shot 2024-06-30 at 10 32 06 PM](https://github.com/quocduyenanhnguyen/Human-trafficking-analysis/assets/92205707/96e3f05a-5ec7-4821-af2f-e28da732dc0a)

-> most victims of sexual exploitation registered in year 2019.

### 7. Countries where victims were exploited
```
SELECT distinct r.Country, count(Datasource) as victim_count FROM global_trafficking_data gd
left join region r on r.iso2 = gd.CountryOfExploitation
group by r.Country
order by victim_count desc
;
```
#### Output
![Screen Shot 2024-06-30 at 10 33 08 PM](https://github.com/quocduyenanhnguyen/Human-trafficking-analysis/assets/92205707/bb758ffb-da2d-45a7-bc8c-deefe928471d)

-> most victims were exploited in the US, while a large volume of victims and their country of exploitation data is missing

### 8. Age group of victims
```
SELECT distinct ageBroad, count(Datasource) as victim_count FROM global_trafficking_data
group by ageBroad
order by victim_count desc
;
```
#### Output
![Screen Shot 2024-06-30 at 10 34 14 PM](https://github.com/quocduyenanhnguyen/Human-trafficking-analysis/assets/92205707/0ba8df9f-2ab1-4f60-95c1-12964c0f5111)

-> most victims' age were not recorded when entering data into the IOM's system. If they were recorded, age 9-17 were trafficked the most.

### 9. majority Status vs majority Status At Exploit of victims
### majority Status
```
SELECT distinct majorityStatus, count(Datasource) as victim_count FROM global_trafficking_data
group by majorityStatus
order by victim_count desc
;
```
#### Output
![Screen Shot 2024-06-30 at 10 34 58 PM](https://github.com/quocduyenanhnguyen/Human-trafficking-analysis/assets/92205707/d462dba3-a52c-4c0a-8829-5a60efca2430)

-> most victims were adults when they seeked help from nonprofits. 

### majority Status At Exploit
```
SELECT distinct majorityStatusAtExploit, count(Datasource) as victim_count FROM global_trafficking_data
group by majorityStatusAtExploit
order by victim_count desc
;
```
#### Output
![Screen Shot 2024-06-30 at 10 35 27 PM](https://github.com/quocduyenanhnguyen/Human-trafficking-analysis/assets/92205707/d30a6b42-b240-451b-abff-347ca14639fa)

-> most data about whether victims were adult or child when they were exploited for the first time are missing. 

### what's their majority status when they seeked help from nonprofits and when they were first exploited? 
```
SELECT distinct majorityStatus, majorityStatusAtExploit, count(Datasource) as victim_count 
FROM global_trafficking_data
where majorityStatus is not null and majorityStatusAtExploit is not null
group by majorityStatus, majorityStatusAtExploit
order by victim_count desc
;
```
#### Output
![Screen Shot 2024-06-30 at 10 36 09 PM](https://github.com/quocduyenanhnguyen/Human-trafficking-analysis/assets/92205707/80545d88-cae2-4058-8c8a-659ca7901ad7)

-> majority of them were minors when they were first exploited and seeked help from nonprofits. Only a small number of victims were exploited as minor and seeked help from nonprofits when they were adults. A lot of missing data makes it challenging to draw a conclusion. It's also possible that victims don't remember past memories or they did not want to provide their age when they seeked help so data were not recorded or missing.

### 10. Victims of both sex and labor abuse by year of registration
```
SELECT distinct yearOfRegistration, count(Datasource) as victim_count 
FROM global_trafficking_data
where isSexAndLabour = 1
group by yearOfRegistration
order by victim_count desc
;
```
#### Output
![Screen Shot 2024-06-30 at 10 37 05 PM](https://github.com/quocduyenanhnguyen/Human-trafficking-analysis/assets/92205707/51f5f9fe-cbd3-44f6-83f3-98795712cf35)

-> most victims can be found in the year 2018. The count is lower than if they were victims of either abuse. 

### 11. Where most abductions take place?
```
SELECT distinct r.Country, count(Datasource) as citizenship_count FROM global_trafficking_data gd
left join region r on r.iso2 = gd.citizenship
where isAbduction = 1
group by r.Country
order by citizenship_count desc
;
```
#### Output
![Screen Shot 2024-06-30 at 10 37 51 PM](https://github.com/quocduyenanhnguyen/Human-trafficking-analysis/assets/92205707/35bd6839-c971-4498-8e0b-0771eade837f)

-> most data are missing and there were only a few abduction cases in the US

### 12. Relationship of recruiters of trafficking to the victims
```
select distinct RecruiterRelationship, count(Datasource) as victim_count
from global_trafficking_data
group by RecruiterRelationship
order by victim_count desc
;
```
#### Output
![Screen Shot 2024-06-30 at 10 39 37 PM](https://github.com/quocduyenanhnguyen/Human-trafficking-analysis/assets/92205707/b042eaa0-3384-453e-94f1-633dc0210af1)

-> Most relationships are not specified or unknown. If they are known, a handful of recruiters are Intimate Partner to the victims.

### 13. Number of human trafficking offenses in California (year is 2022)
```
SELECT distinct niot.offense_name, count(distinct nio.offense_id) as offense_count FROM nibrs_offense nio
join nibrs_offense_type niot on nio.offense_code = niot.offense_code
where lower(niot.offense_name) like lower('%human trafficking%')
group by niot.offense_name
order by offense_count desc
;
```
#### Output
![Screen Shot 2024-06-30 at 10 43 35 PM](https://github.com/quocduyenanhnguyen/Human-trafficking-analysis/assets/92205707/a00aa2c1-062f-44f8-9c22-274f7bda7390)

-> There were 105 cases in 2022 in California. Commercial Sex Acts had the most cases, followed by Involuntary Servitude.

### 14. Number of human trafficking offenses in California (year is 2022) by county name
```
select a.county_name, count(distinct nio.offense_id) as offense_count from agencies a
join nibrs_incident ni on a.agency_id = ni.agency_id
join nibrs_offense nio on nio.incident_id = ni.incident_id
join nibrs_offense_type niot on nio.offense_code = niot.offense_code 
where lower(niot.offense_name) like lower('%human trafficking%')
group by a.county_name
order by offense_count desc
;
```
#### Output
![Screen Shot 2024-06-30 at 10 46 33 PM](https://github.com/quocduyenanhnguyen/Human-trafficking-analysis/assets/92205707/888d7770-39ef-45a3-8219-c55ab0519dfc)

-> Orange county had the most cases

### 15. Where most human trafficking offenses took place in California (year is 2022)? 
```
SELECT distinct nil.location_name, niot.offense_name, count(distinct nio.offense_id) as offense_count FROM nibrs_offense nio
join nibrs_offense_type niot on nio.offense_code = niot.offense_code
join nibrs_location_type nil on nil.location_id = nio.location_id
where lower(niot.offense_name) like lower('%human trafficking%')
group by nil.location_name, niot.offense_name
order by offense_count desc
;
```
#### Output
![Screen Shot 2024-06-30 at 10 47 40 PM](https://github.com/quocduyenanhnguyen/Human-trafficking-analysis/assets/92205707/39199cf2-bc1b-4f89-bbe6-97345001be2c)

-> Most of them took place in a hotel or Motel if it is Commercial Sex Acts. Most of them took place at a house if it is Involuntary Servitude.

### 16. races and genders of trafficking victims in California (year is 2022)? 
```
SELECT distinct rr.race_desc, nv.sex_code as gender, count(distinct nv.victim_id) as victim_count FROM nibrs_offense nio
join nibrs_offense_type niot on nio.offense_code = niot.offense_code
join nibrs_incident ni on ni.incident_id = nio.incident_id
join nibrs_victim nv on nv.incident_id = ni.incident_id
join ref_race rr on rr.race_id = nv.race_id
where lower(niot.offense_name) like lower('%human trafficking%')
group by rr.race_desc, nv.sex_code
order by victim_count desc
;
```
#### Output
![Screen Shot 2024-06-30 at 10 50 35 PM](https://github.com/quocduyenanhnguyen/Human-trafficking-analysis/assets/92205707/0b1a00af-3bd1-4dca-8fd5-5eaa2ce6e378)

-> Most victims were white females, or race not specified and gender is third gender.

### 17. races and genders of trafficking offenders in California (year is 2022)? 
```
SELECT distinct rr.race_desc, niof.sex_code as gender, count(distinct niof.offender_id) as offender_count FROM nibrs_offense nio
join nibrs_offense_type niot on nio.offense_code = niot.offense_code
join nibrs_incident ni on ni.incident_id = nio.incident_id
join nibrs_offender niof on niof.incident_id = ni.incident_id
join ref_race rr on rr.race_id = niof.race_id
where lower(niot.offense_name) like lower('%human trafficking%')
group by rr.race_desc, niof.sex_code
order by offender_count desc
;
```
#### Output
![Screen Shot 2024-06-30 at 10 52 15 PM](https://github.com/quocduyenanhnguyen/Human-trafficking-analysis/assets/92205707/3f34b16e-0b81-40db-aded-ae40ac2f6e00)

-> Most offenders were black or white males.

