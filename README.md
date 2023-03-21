# SQLChallengeCase-3-Foodie-Fi 
<img src="https://user-images.githubusercontent.com/123035903/226533256-42fb7ae8-bb91-4386-b53a-24cbed904df8.png" alt="Image" height="600" width="620">

## :bucket: Table of Contents
- [Background](#background)
- [Entity Relationship Diagram](#entity-relationship-diagram)
- [Table Relationship and Description](#table-relationship-and-description)
- [Case Study Questions](#case-study-questions)
  - [Customer Journey](#customer-journey)
  - [Data Analytics Questions](#data-analytics-questions)
  - [Challenge Payment Question](#challenge-payment-question)
  - [Outside the Box Challenge](#outside-the-box-challenge)
***
## Background

Foodie-Fi, a startup that was launched in 2020 to fill a gap in the market by creating a streaming service that offers food-related content exclusively. The service functions on a subscription-based model, providing customers with unlimited access to a vast range of exclusive food videos from around the world. The founder of Foodie-Fi, Danny, had a data-driven approach in mind when he established the company, aiming to make all investment decisions and introduce new features based on data analysis. This case study focuses on using digital data acquired through Foodie-Fi's subscription model to answer important business questions.
***

## Entity Relationship Diagram
![case-study-3-erd](https://user-images.githubusercontent.com/123035903/226535203-6eb3ca85-38f4-41d9-b068-07e6e2019c85.png)
***

## Table Relationship and Description

All datasets exist within the foodie_fi database schema. This case study focuses on only 2 tables.

### Table 1: plans

Foodie-Fi offers two subscription plans: ``Basic`` and ``Pro``. ``Basic`` plan customers have limited access and can only stream their videos monthly for $9.90. ``Pro`` plan customers have no watch time limits and can download videos for offline viewing. ``Pro`` plans start at $19.90 per month or $199 for an annual subscription. Customers can sign up for a 7-day free trial, which automatically continues with the ``Pro`` monthly subscription plan unless they cancel or downgrade to ``Basic`` or upgrade to an annual ``Pro`` plan. If a customer cancels their subscription, they will have a ``churn`` plan record with a ``null`` price, but their plan will continue until the end of the billing period.

![Screen Shot 2023-03-21 at 5 52 33 pm](https://user-images.githubusercontent.com/123035903/226536234-5acfbf50-b324-4a88-9ff9-644140678daf.png)
***

## Table 2: subscriptions

Customer subscriptions show the exact date where their specific ``plan_id`` starts.

If customers downgrade from a pro plan or cancel their subscription - the higher plan will remain in place until the period is over - the ``start_date`` in the ``subscriptions`` table will reflect the date that the actual plan changes.

When customers upgrade their account from a basic plan to a pro or annual pro plan - the higher plan will take effect straightaway.

When customers churn - they will keep their access until the end of their current billing period but the ``start_date`` will be technically the day they decided to cancel their service.

![Screen Shot 2023-03-21 at 6 01 28 pm](https://user-images.githubusercontent.com/123035903/226537637-a3fc976e-09a9-40a1-abaa-bb4dab8edfa7.png)
***

## Case Study Questions

### Customer Journey
Based off the 8 sample customers provided in the sample from the subscriptions table, write a brief description about each customer’s onboarding journey.
***

### Data Analytics Questions

1. How many customers has Foodie-Fi ever had?
2. What is the monthly distribution of trial plan start_date values for our dataset - use the start of the month as the group by value
3. What plan start_date values occur after the year 2020 for our dataset? Show the breakdown by count of events for each plan_name
4. What is the customer count and percentage of customers who have churned rounded to 1 decimal place?
5. How many customers have churned straight after their initial free trial - what percentage is this rounded to the nearest whole number?
6. What is the number and percentage of customer plans after their initial free trial?
7. What is the customer count and percentage breakdown of all 5 plan_name values at 2020-12-31?
8. How many customers have upgraded to an annual plan in 2020?
9. How many days on average does it take for a customer to an annual plan from the day they join Foodie-Fi?
10. Can you further breakdown this average value into 30 day periods (i.e. 0-30 days, 31-60 days etc)
11. How many customers downgraded from a pro monthly to a basic monthly plan in 2020?
***

### Challenge Payment Question

The Foodie-Fi team wants you to create a new payments table for the year 2020 that includes amounts paid by each customer in the subscriptions table with the following requirements:

- monthly payments always occur on the same day of month as the original start_date of any monthly paid plan
- upgrades from basic to monthly or pro plans are reduced by the current paid amount in that month and start immediately
- upgrades from pro monthly to pro annual are paid at the end of the current billing period and also starts at the end of the month period
- once a customer churns they will no longer make payments
***

### Outside the Box Challenge

The following are open ended questions which might be asked during a technical interview for this case study - there are no right or wrong answers, but answers that make sense from both a technical and a business perspective make an amazing impression!

- How would you calculate the rate of growth for Foodie-Fi?
- What key metrics would you recommend Foodie-Fi management to track over time to assess performance of their overall business?
- What are some key customer journeys or experiences that you would analyse further to improve customer retention?
- If the Foodie-Fi team were to create an exit survey shown to customers who wish to cancel their subscription, what questions would you include in the survey?
- What business levers could the Foodie-Fi team use to reduce the customer churn rate? How would you validate the effectiveness of your ideas?

***
