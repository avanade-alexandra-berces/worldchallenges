# worldchallenges

#sakila
```SQL
USE sakila;
SHOW TABLES;
SELECT * FROM actor;
```

#1. list all actors
```SQL
SELECT first_name, last_name
FROM actor;
```

#2. find the surname of the actor with forename 'John'
```SQL
SELECT last_name
FROM actor
WHERE first_name="John";
```

#3. find all actors with surname 'Neeson'
```SQL
SELECT first_name, last_name
FROM actor
WHERE last_name="Neeson";
```

#4. find all actors with ID numbers divisible by 10
```SQL
SELECT actor_id, first_name, last_name
FROM actor
WHERE actor_id%10=0;
```

#5. what is the description of the movie with an ID of 100
```SQL
DESCRIBE film;

SELECT description
FROM film
WHERE film_id=100;
```

#6. find every R-rated movie
```SQL
SELECT title
FROM film
WHERE rating="R";
```

#7. find every non R-rated movie
```SQL
SELECT title
FROM film
WHERE rating<>"R";
```

#8. find the ten shortest movies
```SQL
SELECT title, length
FROM film
ORDER BY length ASC LIMIT 0,10;
```

#9. find the movies with the longest runtime without using LIMIT
```SQL
#need to ask if this is supposed to be the 10 longest movies
SELECT title
FROM film
WHERE length=(SELECT MAX(length) FROM film);
```

#10. find all movies that have deleted scenes
```SQL
SELECT title
FROM film
WHERE special_features="Deleted Scenes";
```

#11. using HAVING, reverse-alphabetically list the last names that are not repeated
```SQL
SELECT last_name FROM actor
GROUP BY last_name
HAVING COUNT(last_name)=1
ORDER BY last_name DESC;
```

#12. using HAVING, list the last names that appear more than once from highest to lowest frequency
```SQL
SELECT last_name FROM actor
GROUP BY last_name
HAVING COUNT(last_name)>1
ORDER BY COUNT(last_name) DESC;
```

#13. which actor has appeared in the most films?
```SQL
SELECT actor_id
FROM film_actor
GROUP BY actor_id
ORDER BY COUNT(actor_id) DESC LIMIT 1;

SELECT first_name, last_name
FROM actor
WHERE actor_id=107; #Gina Degeneres
```

#14. when is 'Academy Dinosaur' due?
```SQL
SELECT release_year
FROM film
WHERE title="Academy Dinosaur";
```

#15. what is the average runtime of all films?
```SQL
SELECT AVG(length)
FROM film;
```

#16. list the average runtime for every film category
```SQL
SELECT AVG(length), category.name
FROM film
JOIN film_category ON film_category.film_id=film.film_id
JOIN category ON film_category.category_id=category.category_id
GROUP BY film_category.category_id;
```

#17. list all movies featuring a robot
```SQL
SELECT title FROM film
WHERE description LIKE "%Robot%";
```

#18. how many movies were released in 2010?
```SQL
SELECT COUNT(title)
FROM film
WHERE release_year=2010;
```

#19. find the titles of all the horror movies
```SQL
SELECT title, category.name
FROM film
JOIN film_category ON film_category.film_id=film.film_id
JOIN category ON film_category.category_id=category.category_id
WHERE category.name="Horror";
```

#20. list the full names of the staff member with the ID of 2
```SQL
SELECT first_name, last_name
FROM staff
WHERE staff_id=2;
```

#21. list all the movies that Fred Costner has appeared in
```SQL
SELECT title
FROM film JOIN film_actor ON film_actor.film_id=film.film_id
JOIN actor ON actor.actor_id=film_actor.actor_id
WHERE actor.first_name='Fred' AND actor.last_name='Costner';
```

#22. how many distinct countries are there?
```SQL
SELECT COUNT(DISTINCT country)
FROM country;
```

#23. list the name of every language in reverse-alphabetical order
```SQL
SELECT name FROM language
ORDER BY name DESC;
```

#24. list the full names of every actor whose names ends with '-son' in alphabetical order by their forename
```SQL
SELECT first_name, last_name
FROM actor WHERE last_name LIKE "%son"
ORDER BY first_name ASC;
```

#25. which category contains the most films?
```SQL
SELECT category.name
FROM category
JOIN film_category ON category.category_id=film_category.category_id
GROUP BY category.name
ORDER BY COUNT(film_category.category_id) DESC LIMIT 1;
```
