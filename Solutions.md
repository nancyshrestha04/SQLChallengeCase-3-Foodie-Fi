# 🗒️Solutions

## A. Customer Journey

### Based off the 8 sample customers provided in the sample from the subscriptions table, write a brief description about each customer’s onboarding journey.

- Customer ID 1 initiated their subscription journey with a trial subscription and eventually upgraded to Basic Monthly subscription within 7 days of sign up.
- Customer ID 2 started their subscription journey with a trial subscription and then upgraded to Pro annual subscription within 7 days of sign up.
- Customer ID 11 discontinued their subscription journey within 7 days of free trial. 
- Customer with ID 13 started their subscription journey with a trial subscription and then upgraded to a basic monthly subscription within seven days of sign-up. Within seven days of upgrading to the basic monthly subscription, they further upgraded to a pro monthly subscription.
- Customer ID 15 started with the free trial subscription, upgraded to Pro Monthly plan after 7 days of sign up and then discontinued the subscription after a month.
- Customer ID 16 initiated their subscription journey with a trial subscription and subsequently upgraded to a basic monthly subscription within seven days of sign-up. After four months they upgraded to a pro annual subscription.
- Customer with ID 18 began their subscription journey with a trial subscription and subsequently upgraded to a pro monthly subscription within seven days of sign-up.
- Customer with ID 19 started their subscription journey with a trial subscription and subsequently upgraded to a pro monthly subscription within seven days of sign-up. After two months of being on the pro monthly subscription, they further upgraded to a pro annual subscription.
***

## B. Data Analysis Questions

### 1. How many customers has Foodie-Fi ever had?
````sql
 SELECT  count(distinct customer_id) as total_customers
 FROM    subscriptions;
````
| total_customers |
| --------------- |
| 1000            |
***

### 2. What is the monthly distribution of trial plan `start_date` values for our dataset - use the start of the month as the group by value.
````sql
SELECT		extract(month from start_date) as month_date,
			TO_CHAR(start_date, 'Month') as monthly_distribution,
			count(*)	as no_of_customers		
FROM 		subscriptions
Where		plan_id = 0
GROUP BY	month_date,monthly_distribution
ORDER BY	month_date;
````
![trial_subscription](https://user-images.githubusercontent.com/123035903/227854793-58c2d69a-99e0-4b0d-b420-def0340a635a.png)
***

### 3. What plan start_date values occur after the year 2020 for our dataset? Show the breakdown by count of events for each plan_name.
````sql
SELECT		p.plan_id, p.plan_name, count(*) as total_number_of_events			
FROM		subscriptions s
			 JOIN plans p 
			 ON s.plan_id = p.plan_id
WHERE		s.start_date > '2020-12-31'
GROUP BY	p.plan_id, p.plan_name
ORDER BY	p.plan_id, p.plan_name;
````
![events](https://user-images.githubusercontent.com/123035903/227860234-b7a366a7-25be-42e1-8f2d-e3c842c72886.png)
***
### 4. What is the customer count and percentage of customers who have churned rounded to 1 decimal place?
````sql
SELECT		count(customer_id) as churn_count,
			ROUND(100 * count(customer_id)::NUMERIC/(
SELECT		COUNT(DISTINCT customer_id) 
FROM 		subscriptions),1) AS churn_count_percentage
FROM		subscriptions s
				JOIN plans p
				ON s.plan_id = p.plan_id
WHERE		p.plan_name = 'churn' and s.start_date IS NOT NULL;
````
![Screen Shot 2023-03-27 at 6 45 34 pm](https://user-images.githubusercontent.com/123035903/227875246-83ea305c-4bfa-45d5-b33c-a14d912eff5e.png)
***

### 5. How many customers have churned straight after their initial free trial - what percentage is this rounded to the nearest whole number?
````sql

WITH ranking AS (
SELECT	s.customer_id, s.plan_id, p.plan_name,
		ROW_NUMBER() OVER (
    	PARTITION BY s.customer_id 
    	ORDER BY s.plan_id) AS plan_rank 
FROM	subscriptions s
		JOIN plans p
  		ON s.plan_id = p.plan_id
)  
SELECT	COUNT(*) AS churn_count,
  		ROUND(100 * COUNT(*) / (
    	SELECT COUNT(DISTINCT customer_id) 
    	FROM subscriptions),0) AS churn_percentage
FROM	ranking
WHERE	plan_id = 4 
  		AND plan_rank = 2;
````
![Screen Shot 2023-03-27 at 8 05 12 pm](https://user-images.githubusercontent.com/123035903/227895263-6e1cd590-55b7-4b62-955a-afa64774ca80.png)
***

### 6. What is the number and percentage of customer plans after their initial free trial?



