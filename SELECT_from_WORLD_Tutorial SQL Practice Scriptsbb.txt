SQL Practice 

SELECT statements paractice from WORLD Tutorial: https://sqlzoo.net/wiki/SELECT_within_SELECT_Tutorial

1.List each country name where the population is larger than that of 'Russia'.

SELECT name FROM world
  WHERE population >
     (SELECT population FROM world
      WHERE name='Russia')
	  
Correct answer

name
Bangladesh
Brazil
China
India
Indonesia
Nigeria
Pakistan
United States

2.Show the countries in Europe with a per capita GDP greater than 'United Kingdom'.

SELECT name FROM world WHERE continent = 'Europe' and gdp/population   > 
 (SELECT gdp/population FROM world WHERE name = 'United Kingdom')
 
Correct answer 

name
Andorra
Austria
Belgium
Denmark
Finland
France
Germany
Iceland
Ireland
Liechtenstein
Luxembourg
Monaco
Netherlands
Norway
San Marino
Sweden
Switzerland

3.List the name and continent of countries in the continents containing either Argentina or Australia. Order by name of the country.

Select name,continent  FROM world WHERE continent  in 
(SELECT continent FROM world WHERE name IN ('Argentina','Australia'))


Correct answer

name	                           continent
Argentina                          South America
Australia	                       Oceania
Bolivia	                           South America
Brazil	                           South America
Chile	                           South America
Colombia	                       South America
Ecuador	                           South America
Fiji	                           Oceania
Guyana	                           South America
Kiribati	                       Oceania
Marshall Islands	               Oceania
Micronesia, Federated States of	   Oceania
Nauru	                           Oceania
New Zealand	                       Oceania
Palau	                           Oceania
Papua New Guinea	               Oceania
Paraguay	                       South America
Peru	                           South America
Saint Vincent and the Grenadines   South America
Samoa	                           Oceania
Solomon Islands	                   Oceania
Suriname	                       South America
Tonga	                           Oceania
Tuvalu	                           Oceania
Uruguay	                           South America
Vanuatu	                           Oceania
Venezuela	                       South America

4.Which country has a population that is more than United Kingom but less than Germany? Show the name and the population.

SELECT name,population FROM world WHERE population > 
(SELECT population FROM world WHERE name = 'United Kingdom') 
AND population < (SELECT population FROM world WHERE name = 'Germany') 

Correct answer

name	                        population
Congo, Democratic Republic of	69360000
France	                        65906000
Iran	                        77552000
Thailand	                    64456700
Turkey	                        76667864

5.Show the name and the population of each country in Europe. Show the population as a percentage of the population of Germany.


SELECT name,CONCAT(ROUND(population/80000000 * 100.0,0) , '%') AS percentage  
FROM world WHERE continent = 'Europe'

6.Show the name and the population of each country in Europe. Show the population as a percentage of the population of Germany.

SELECT name,
CONCAT(ROUND(population/80000000 * 100.0,0),'%') AS percentage
FROM world 
WHERE continent = 'Europe'

Wrong answer. Some of the data is incorrect.

name	                   percentage
Albania                    4.0000000000%
Andorra	                   0.0000000000%
Austria                   11.0000000000%
Belarus	                  12.0000000000%
Belgium	                  14.0000000000%
Bosnia and Herzegovina     5.0000000000%
Bulgaria	               9.0000000000%
Croatia	                   5.0000000000%
Czech Republic	          13.0000000000%
Denmark	                   7.0000000000%
Estonia	                   2.0000000000%
Finland	                   7.0000000000%
France	                  82.0000000000%
Germany                  101.0000000000%
Greece					  14.0000000000%
Hungary					  12.0000000000%
Iceland					   0.0000000000%
Ireland	                   6.0000000000%
Italy	                  76.0000000000%
Kazakhstan	              22.0000000000%
Latvia	                   2.0000000000%
Liechtenstein              0.0000000000%
Lithuania	               4.0000000000%
Luxembourg	               1.0000000000%
Macedonia	               3.0000000000%
Malta	                   1.0000000000%
Moldova                    4.0000000000%
Monaco	                   0.0000000000%
Montenegro                 1.0000000000%
Netherlands            	  21.0000000000%
Norway	                   6.0000000000%
Poland	                  48.0000000000%
Portugal	              13.0000000000%
Romania	                  25.0000000000%
San Marino                 0.0000000000%
Serbia	                   9.0000000000%
Slovakia	               7.0000000000%
Slovenia	               3.0000000000%
Spain	                  58.0000000000%
Sweden	                  12.0000000000%
Switzerland               10.0000000000%
Ukraine	                  54.0000000000%
United Kingdom	          80.0000000000%
Vatican City	           0.0000000000%


6.Which countries have a GDP greater than every country in Europe? [Give the name only.] (Some countries may have NULL gdp values)

SELECT name 
FROM world 
WHERE gdp > ALL(select gdp from world where gdp > 0 and continent = 'Europe')

Correct answer

name
China
Japan
United States


7.Find the largest country (by area) in each continent, show the continent, the name and the area:

SELECT continent, name, area 
FROM world x
WHERE area >= ALL
    (SELECT area FROM world y
        WHERE y.continent=x.continent
          AND area>0)

Correct answer 

continent	       name 	area
Africa	         Algeria	 2381741
Oceania     	 Australia	 7692024
South America	 Brazil	     8515767
North America	 Canada    	 9984670
Asia	         China	     9596961
Caribbean	     Cuba	      109884
Europe	         Kazakhstan	 2724900
Eurasia	         Russia	    17125242


8.List each continent and the name of the country that comes first alphabetically.

SELECT continent, name
FROM   ( SELECT Row_number() OVER(partition BY continent ORDER BY name) Rn,
        continent, name from world) A
WHERE  rn = 1 


Correct answer

continent	     name
Africa	         Algeria
Asia	         Afghanistan
Caribbean	     Antigua and Barbuda
Eurasia	         Armenia
Europe	         Albania
North America	 Belize
Oceania	         Australia
South America	 Argentina


9.Find the continents where all countries have a population <= 25000000. 
  Then find the names of the countries associated with these continents. Show name, continent and population.
  
SELECT name, continent, population 
FROM world x
WHERE 25000000>=ALL (SELECT population FROM world y
                         WHERE x.continent=y.continent
                         AND population>0)
						 
Correct answer

name	                            continent	population
Antigua and Barbuda	   				Caribbean	   	86295
Australia	           				Oceania	     23545500
Bahamas	               				Caribbean	   351461
Barbados	           				Caribbean	   285000
Cuba	               				Caribbean	 11167325
Dominica	           				Caribbean	    71293
Dominican Republic	   				Caribbean	  9445281
Fiji	               				Oceania	       858038
Grenada	               				Caribbean	   103328
Haiti	               				Caribbean	 10413211
Jamaica	               				Caribbean	  2717991
Kiribati	           				Oceania	       106461
Marshall Islands	                Oceania         56086
Micronesia, Federated States of 	Oceania	       101351
Nauru	                            Oceania	         9945
New Zealand	                        Oceania	       4538520
Palau	                            Oceania	         20901
Papua New Guinea	                Oceania	       7398500
Saint Lucia	                        Caribbean	    180000
Samoa	                            Oceania	        187820
Solomon Islands	                    Oceania	         581344
Tonga	                            Oceania	         103036
Trinidad and Tobago	                Caribbean	     1328019
Tuvalu	                            Oceania	           11323
Vanuatu	                            Oceania	           264652


10.Some countries have populations more than three times that of all of their neighbours (in the same continent). 
   Give the countries and continents.
   
SELECT name, continent
FROM world x
WHERE population > ALL(SELECT population*3 FROM world y WHERE x.continent = y.continent AND population > 0 AND y.name != x.name)  

Correct answer

name	    continent
Russia	    Eurasia
Australia	Oceania
Brazil	    South America

   
						 