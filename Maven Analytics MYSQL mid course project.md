/* DATE CREATED: AUGUST 22ND 2023
CREATED BY: ABHIRAJ SINGH DADIYAN
DESCRIPTION: MAVEN ANALYTICS MID COURSE PROJECT
SITUATION: The company's insurance policy is up for renewal and the insurance company's underwriters 
need some updated information from us before they will issue new policy. They have four questions 
for which we will be querying our database and providing answers */

/*Question 1: We will need a list of all staff members, including their first and last names,
 email addresses and the store identification number where they work */

SELECT
	 first_name
	,last_name
    ,email
    ,store_id
FROM
	staff;

/* Question 2: We will need sperate counts of inventory items held at each of your two stores */

SELECT
	 store_id
	,COUNT(inventory_id) AS inventory_count
FROM
	inventory
GROUP BY
	store_id;

/*Question 3: We will need a count of active customers for each of your stores seperately */

SELECT
	 store_id
	,COUNT(customer_id) AS active_customers
FROM
	customer
WHERE
	active = 1
GROUP BY
	store_id;

/* Question 4: In order to assess the liability of data breach, we will need you to provide a count of all 
customer email addresses stored in the database */

SELECT
	COUNT(email)
FROM
	customer;

/* Question 5: We are interested in how diverse your film offering is as a means of understanding how likely
 you are to keep customers engaged in future.Provide a count of unique film titles you have in inventory at 
 each store and then produce a count of unique categories of films you provide */

-- Number of Unique film titles

SELECT
	 store_id
	,COUNT(DISTINCT(film_id)) AS Number_of_Unique_film_titles
FROM
	inventory
GROUP BY
	store_id;
    
-- Number of unique categories

SELECT
	COUNT(DISTINCT(name)) AS number_of_unique_categories
FROM
	category;
    
/* Question 6: We would like to understand the replacement cost of your films. Please provide the replacement cost for the
 film that is least expensive to replace, most expensive to replace, and the average replacement cost */

SELECT
	 MIN(replacement_cost) AS Cheapest_replacement_cost
    ,MAX(replacement_cost) AS Highest_replacement_cost
    ,AVG(replacement_cost) AS Average_replacement_cost
FROM
	film;

/*Question 7: We are interested in having you put payment monitoring systems and maximum payment processing restrictions in
 place in order to minimize the future risk of fraud by your staff. Provide the avergae payment you process
 as well as the maximum payment you have processed */
 
 SELECT
	 MAX(amount) AS Max_payment
	,AVG(amount) AS Average_payment
FROM
	payment;
    
/*Question 8: We would like to better understand what your customer base looks like. Provide a list of all
customer identification values, with a count of rentals they have made all time, with your highest volume
customers at top of the list */

SELECT
	 customer_id
	,COUNT(rental_id) as number_of_rentals
FROM
	rental
GROUP BY
	customer_id
ORDER BY
	COUNT(rental_id) DESC;
