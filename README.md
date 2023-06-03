SELECT *
FROM movieset-386712.movies_set.explore_movie


-- SELECTING THE NEEDED DATA FOR EXPLORATION



SELECT movie_title AS title, Release_Date As release_date,Genre__1_ AS genre, Director__1_ AS director, Budget____ AS budget, Box_Office_Revenue____ AS revenue
FROM movieset-386712.movies_set.explore_movie


-- SAVING THE SELECTED DATA AS BETA_MOVIES_SET USING THE WITH FUNCTION

WITH beta_movies_set AS (SELECT movie_title AS title, Release_Date As release_date,Genre__1_ AS genre, Director__1_ AS director, Budget____ AS budget, Box_Office_Revenue____ AS revenue
FROM movieset-386712.movies_set.explore_movie 
)

SELECT *
FROM beta_movies_set


-- counting movies by genre

SELECT genre,COUNT(*) AS moviebygenre
FROM movies_set.beta_movies_set
GROUP BY 1
ORDER BY 2 DESC


--  CHECKING THE TOP 10 DIRECTORS WITH MOST MOVIE DIRECT

SELECT director, COUNT(title) AS movie_count
FROM movies_set.beta_movies_set
GROUP BY director
ORDER BY movie_count DESC
LIMIT 10


-- LOOKING INTO Drama movies using the LIKE function

SELECT title, genre
FROM movies_set.beta_movies_set
WHERE genre like '%ma'
ORDER BY 1



-- Looking into the top 10 movie genre with most movie and Revenue

SELECT genre, COUNT(*) AS genrecount, SUM(revenue) AS TotalGenreRevenue
FROM movies_set.beta_movies_set
GROUP BY 1
ORDER BY 2 DESC
LIMIT 10;

-- Looking into Action movie release by year

SELECT *
FROM(
SELECT DATE_TRUNC(release_date, year) AS release_year, genre, COUNT(*) AS total_movies
FROM movies_set.beta_movies_set
GROUP BY 1, 2
ORDER BY total_movies, release_year DESC)
WHERE genre = 'Action'


-- Checking the Top 10 movie genre with most Revenue

SELECT genre,SUM(revenue) AS totalRevenue
FROM movies_set.beta_movies_set
GROUP BY genre
ORDER BY totalRevenue DESC
LIMIT 10


-- Checking the Average Budget and Revenue for All movies Genre

SELECT genre, AVG(revenue) *100 AS AverageRevenue, AVG(budget) *100 AS AverageBudget
FROM movies_set.beta_movies_set
GROUP BY genre
ORDER BY AverageRevenue, AverageBudget DESC


-- movie count by director

SELECT director, COUNT(title) AS movie_count
FROM movies_set.beta_movies_set
GROUP BY director
ORDER BY movie_count DESC
LIMIT 50

SELECT * 
FROM movies_set.explore_movie
