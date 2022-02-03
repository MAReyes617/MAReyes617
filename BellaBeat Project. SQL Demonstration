/* FitBit Data Exploration w/BigQuery SQL

Goal of project was to gather insight on 33 fitbit users. How can their recorded usage, for 31 days, help Bellabeat offer a better product/experience  

Skills used: Joins, CTE's, Functions, Aggregate Functions, Adding Data Types, Boolean, Alter/Modifying Table(s) 


*/



-- how many steps did the focus group take combined ?

SELECT SUM(TotalSteps)  AS TotalGroupSteps
FROM `my-final-project-59674.fitabase_data.daily_activity` 


-- who averaged the most lightly active minutes ?

SELECT Id, AVG(LightlyActiveMinutes) AS OverallActiveMinutes
FROM `my-final-project-59674.fitabase_data.daily_intensities`
GROUP BY Id
ORDER BY OverallActiveMinutes DESC

-- query to help gather information just on users active minutes and sum them all together

SELECT Id, SUM(LightlyActiveMinutes), SUM(FairlyActiveMinutes), SUM(VeryActiveMinutes)
FROM `my-final-project-59674.fitabase_data.daily_intensities`
GROUP BY Id 

SELECT Id, SUM(LightlyActiveMinutes + FairlyActiveMinutes + VeryActiveMinutes)
FROM `my-final-project-59674.fitabase_data.daily_intensities`
GROUP BY Id 

-- who burned the most calories ?

SELECT Id, SUM(Calories) AS TotalCaloriesBurned
FROM `my-final-project-59674.fitabase_data.daily_calories`
GROUP BY Id
ORDER BY TotalCaloriesBurned DESC

-- JOIN daily calories table with daily steps to view relation 
SELECT * FROM `my-final-project-59674.fitabase_data.daily_calories` calories
FULL OUTER JOIN `my-final-project-59674.fitabase_data.daily_steps` steps
ON calories.Id = steps.Id

-- Who slept the most ?

SELECT Id, SUM(TotalMinutesAsleep) AS TotalTimeAsleep
FROM `my-final-project-59674.fitabase_data.sleep_logs`
GROUP BY Id
ORDER BY TotalTimeAsleep DESC
LIMIT 1

-- user w/id 5553957443 lead group with highest totaltimeasleep clocking in with 14368 minutes. 
-- used basic function underneath to divide total time by 31 days. duration of whole data collection period

SELECT (14368/31)


-- Who slept the least amount ?

SELECT Id, SUM(TotalMinutesAsleep) AS TotalTimeAsleep
FROM `my-final-project-59674.fitabase_data.sleep_logs`
GROUP BY Id
ORDER BY TotalTimeAsleep ASC
LIMIT 1

--user w/ id 2320127002 clocked in with the least amount of sleep w 61 totaltimeasleep. low number caused concern
-- this lead me to discover that sleep feature has not been utilized by all users nor on a consistent basis

SELECT *
FROM `my-final-project-59674.fitabase_data.sleep_logs`
WHERE Id = 2320127002


SELECT DISTINCT SleepDay, TotalMinutesAsleep
FROM `my-final-project-59674.fitabase_data.sleep_logs`
WHERE Id = 5553957443


-- how many times do users use the sleep log feature ?

SELECT Id, COUNT(TotalSleepRecords) AS UserCheckins
FROM `my-final-project-59674.fitabase_data.sleep_logs`
GROUP BY Id
ORDER BY UserCheckins DESC

-- JOIN combining both tables daily activity with sleep log for analysis
SELECT * FROM `my-final-project-59674.fitabase_data.daily_activity` activity
LEFT OUTER JOIN  `my-final-project-59674.fitabase_data.sleep_logs` sleep
ON activity.Id = sleep.Id


-- now for weight logs, we would like to learn if users manually entering weigh or are they using fitbit scale connected to fitbit.com ?

/* project's data directionary describes boolean If the data for this weigh in was done manually
(TRUE), or if data was measured and synched
directly to Fitbit.com from a connected scale
(FALSE) */


-- need to quantify the amount of times weight log feature was used. alter table by adding column

ALTER TABLE `my-final-project-59674.fitabase_data.weight_logs`
ADD COLUMN TotalWeightRecords INT64

-- insert default value of 1 to newly created column 

INSERT INTO `my-final-project-59674.fitabase_data.weight_logs`(TotalWeightRecords)
VALUES ('1')


-- to keep things tidy, will remove new column TotalWeightsRecords since it was only valuable to this particular data exploration

ALTER TABLE `my-final-project-59674.fitabase_data.weight_logs`
DROP COLUMN TotalWeightRecords

-- could not complete weight log insight due to limitations of free bigquery sql prohibiting dml statements
