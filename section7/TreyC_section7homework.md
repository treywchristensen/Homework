# Section 7.1 
## Question 1 - Using EVregistry, Write a query to select the ModelYear, Make, and Model off all of the vehicles in the registry.
```SQL

SELECT ModelYear, Make, Model from EVRegistry 

```
## Question 2 - Using the EVRegistry table, Write a query that lists all of the unique types of EV's. your reult set should have one column, ElectricVehicleType.
```SQL

SELECT DISTINCT ElectricVehicleType from EVRegistry

```
## Question 3 - Using the EVRegistry, Write a query that shows all of the information on Battery Electric Vehicles (BEV) that are in the registry.
```SQL

SELECT * FROM EVRegistry Where ElectricVehicleType = 'Battery Electric Vehicle (BEV)' 

```
## Question 4 - Using the EVRegistry, wirte a query that returns the Make and Model of all of the EV's that have a BaseMSRP between 20000 and 35000?
```SQL

SELECT Make, Model from EVRegistry WHERE BaseMSRP BETWEEN 20000 AND 35000 

```

# Section 7.2 
## Question 1 - Using EVRegistry, write a query to find a record where the City attribute is NULL. Return all of the available columns.
```SQL

SELECT * FROM EVRegistry Where City IS NULL

```
## Question 2 - Write a query to find the make, model, and ElectricVehicleType where the VIN number has that ends in '3E1EA1J'.
```SQL

SELECT Make, Model, ElectricVehicleType FROM EVRegistry WHERE VIN LIKE '%3E1EA1J'

```
## Question 3 - Select the ModelYear, make, model, ElectricVehicleType, and range of the Tesla vehicles or cheverolet vehicles in the registry. Order the result set by Make and Model year in from newest to oldest.
```SQL

SELECT ModelYear, Make, Model, ElectricVehicleType, ElectricRange
FROM EVRegistry
WHERE Make IN ('CHEVROLET','TESLA')
ORDER BY Make, ModelYear DESC

```
## Question 4 - Using EVCharging, Write a query to find out how many many times those stations were used. Order them by the most used to the least used and limit the output to 5 records.
```SQL

SELECT stationId, count(stationid) as 'count'
FROM EVCharging
GROUP BY stationId
ORDER BY count DESC
LIMIT 5

```
## Question 5 - Using EVCharging, For the folks who charged longer than 0.5 hours, show the min and max of the charging time for each user. Your output columns should be userid, minTime, and maxTime. Order this result set by the last two columns respectively.
```SQL

SELECT userId, MIN(chargeTimeHrs) as 'minTime', MAX(chargeTimeHrs) as 'maxTime'
FROM EVCharging
WHERE chargeTimeHrs > .5 
GROUP BY userId
ORDER BY 2,3

```

# Section 7.3 
## Question 1 - Using EVCharging, Which day of the week has the highest average charging time? Round the answer to 2 decimal points.
```SQL

SELECT weekday, round(AVG(chargeTimeHrs),2) as AvgChargeTime
FROM EVCharging
GROUP BY weekday
ORDER BY AvgChargeTime DESC
LIMIT 1

```
## Question 2 - Using, EV charging, Find the total power consumed from charging EV's by each User. Return the userId and name the calculated column, totalPower. Round the answer to 2 deciaml points and list the out put in highest to lowest order. Limit the order to the top 15 users.
```SQL

SELECT userId, sum(kwhTotal) as totalPower
from EVCharging
group by userId
order by round(totalpower, 2) DESC
limit 15

```
## Question 3 - Select the ModelYear, make, model, ElectricVehicleType, and range of the Tesla vehicles or cheverolet vehicles in the registry. Order the result set by Make and Model year in from newest to oldest.
```SQL

SELECT df.typeFacility, count(DISTINCT fc.stationId) as numstation
FROM factCharge fc
JOIN dimFacility df on df.FacilityKey = fc.facilityID
GROUP By df.typeFacility
ORDER By numstation DESC

```
## Question 4 - In your own words, Briefly explain Primary Keys and Foreign Keys.


**The Primary Key uniquely identifies each record in the table - ALl values are unique and do not contain NULL values.**

**The Foreign Key is used to connect to other tables. It is used to identify the primary key in a connected table.**


## Question 5 - Using EV Charging, For the folks who charged longer than one hour, show the min and max of the charging time for each user. Your output columns should be userid, minTime, and maxTime. Order this result set by the last two columns respectively. HINT: USE HAVING
```SQL

SELECT userId, min(chargeTimeHrs) as minTime, max(chargetimeHrs) as maxTime
FROM EVCharging
GROUP BY userId
Having minTime > 1
ORDER BY 2,3

```