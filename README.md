# Exercices mySQL par Jaouad ASSABBOUR 


Ceci n'est pas une liste exaustive, toutefois elle présente une partie de mon idée, des pages d'exercices sont disponibles.<br>
La requête:
-----------

**Quelle requête utiliser pour afficher l'ensemble des enregistrements de la table lpecom_livres ?**

```
SELECT name, zip_code FROM lpecom_cities WHERE gps_lat= 48.66913724637683 AND gps_lng=1.87586057971015;
```
----------------------------- ----------
| name                        | zip_code |
-----------------------------:|:----------
| Vieille-├ëglise-en-Yvelines  | 78125    |
---------------------------------------

 **Sans jointure, quelle requête utiliser pour calculer le nombre de villes que compte le département de
 l'Essonne ?**
```
SELECT COUNT(department_code) FROM lpecom_cities WHERE department_code=91;
```
------------------------
| COUNT(department_code) |
:------------------------:
|                    197 |
------------------------

** Sans jointure, quelle requête utiliser pour calculer le nombre de villes en Île-de-France se terminant
 par '-le-Roi' ?**
 ```
 SELECT COUNT(name) FROM lpecom_cities WHERE name LIKE '%-le-Roi';
```
-------------
| COUNT(name) |
:-------------:
|          11 |
-------------

**Combien de villes possèdent le code postal (zip_code) 77320 ? Renommez la colonne de résultat
 n_cities ?**
 ```
 SELECT COUNT(zip_code) AS MY_CITY FROM lpecom_cities WHERE zip_code='77320';
```
---------
| MY_CITY |
:---------:
|      22 |

**Sans jointure, quelle requête utiliser pour calculer le nombre de villes commençant par 'Saint-' en
 Seine-et-Marne ?**
```
SELECT COUNT(name) FROM lpecom_cities WHERE name LIKE 'Saint-%' AND department_code ='77';
```

| COUNT(name) |
:-------------:
|          36 |

**Quelles villes possèdent un code postal (zip_code) compris entre 77210 et 77810 ?**

```SELECT name FROM lpecom_cities WHERE zip_code BETWEEN '77210' AND '77810';```

**Sans jointure, quelles sont les deux villes de Seine-et-Marne à avoir le code postal (zip_code) le
 plus grand ?**
```
SELECT name FROM lpecom_cities ORDER BY zip_code DESC LIMIT 2;
```

| name              |
:-------------------:
| Enghien-les-Bains |
| Bezons            |


**Quel est le code postal (zip_code) le plus grand de la table lpecom_cities ?**

```
SELECT MAX(zip_code) FROM lpecom_cities;
```

| MAX(zip_code) |
:---------------:
| 95880         |

**Quelle requête utiliser pour obtenir en résultat, les noms de la région, du département et de chaque
 ville du département ayant pour code 77 ?**
```
SELECT lpecom_departments.code, lpecom_cities.name, lpecom_regions.name FROM lpecom_regions JOIN lpecom_departments ON lpecom_regions.code = lpecom_departments.region_code JOIN lpecom_cities ON lpecom_departments.code = lpecom_cities.department_code WHERE lpecom_departments.code= 77;
```

| code | name                        | name           |
:-----:|:---------------------------:|:---------------:
| 77   | Ach├¿res-la-For├¬t          | ├Äle-de-France  |
| 77   | Amillis                     | ├Äle-de-France  |
| 77   | Amponville                  | ├Äle-de-France  |
| 77   | Andrezel                    | ├Äle-de-France  |
| 77   | Annet-sur-Marne             | ├Äle-de-France  |

**Quelle requête utiliser pour afficher toutes les données de vaccination uniquement pour le 1er avril
 2021 ? **
```
 SELECT * FROM lpecom_covid WHERE jour = '2021-04-01';
```

| id   | id_region | jour       | n_dose1 | n_dose2 | n_cum_dose1 | n_cum_dose2 | couv_dose1 | couv_dose2 |
:-----:|:---------:|:----------:|:-------:|:-------:|:-----------:|:-----------:|:----------:|:-----------:
|   96 | 01        | 2021-04-01 |     425 |     160 |       10200 |        3834 |       2.70 |       1.00 |
|  197 | 02        | 2021-04-01 |     889 |     160 |       14579 |        5088 |       4.10 |       1.40 |
|  298 | 03        | 2021-04-01 |     331 |     267 |        9812 |        4550 |       3.40 |       1.60 |
|  399 | 04        | 2021-04-01 |     676 |     698 |       38033 |       20045 |       4.40 |       2.30 |
|  500 | 06        | 2021-04-01 |     191 |     106 |        9289 |        4304 |       3.30 |       1.50 |
|  601 | 07        | 2021-04-01 |      58 |      30 |         647 |         230 |       6.50 |       2.30 |
|  702 | 08        | 2021-04-01 |      55 |      45 |        1181 |         642 |       3.30 |       1.80 |
|  803 | 11        | 2021-04-01 |   42359 |   19709 |     1398310 |      400046 |      11.40 |       3.30 |
|  904 | 24        | 2021-04-01 |   11786 |    3071 |      328935 |      128834 |      12.90 |       5.00 |
| 1005 | 27        | 2021-04-01 |   13868 |    3758 |      426598 |      154511 |      15.30 |       5.60 |
| 1106 | 28        | 2021-04-01 |   17181 |    5110 |      483475 |      159637 |      14.60 |       4.80 |
| 1207 | 32        | 2021-04-01 |   17501 |   10004 |      819580 |      224681 |      13.70 |       3.80 |
| 1308 | 44        | 2021-04-01 |   22720 |    8593 |      791990 |      270775 |      14.40 |       4.90 |
| 1409 | 52        | 2021-04-01 |   18219 |    3305 |      465913 |      163045 |      12.30 |       4.30 |
| 1510 | 53        | 2021-04-01 |   17518 |    3965 |      478127 |      171912 |      14.30 |       5.10 |
| 1611 | 75        | 2021-04-01 |   33921 |    6380 |      899615 |      313916 |      15.00 |       5.20 |
| 1712 | 76        | 2021-04-01 |   32981 |    5157 |      823665 |      296753 |      13.90 |       5.00 |
| 1813 | 84        | 2021-04-01 |   35047 |    9568 |     1045812 |      348968 |      13.00 |       4.30 |
| 1914 | 93        | 2021-04-01 |   27929 |    7182 |      762341 |      253866 |      15.10 |       5.00 |
| 2015 | 94        | 2021-04-01 |    1593 |     650 |       61435 |       22805 |      17.80 |       6.60 |

**Quelle requête utiliser pour afficher le nombre au cumulé de vaccination première dose par
 régions en 2020 ?**
```
SELECT r.name, sum(n_dose1) AS TOTAL FROM lpecom_covid c INNER JOIN lpecom_regions r ON c.id_region = r.code GROUP BY r.name ORDER BY jour LIKE '%2020';
```

| name                        | TOTAL   |
:----------------------------:|:--------:
| Grand Est                   |  836877 |
| Guadeloupe                  |   10503 |
| Pays de la Loire            |  501833 |
| Martinique                  |   18330 |
| Bretagne                    |  515527 |
| Guyane                      |   10572 |
| Nouvelle-Aquitaine          |  976357 |
| La R├®union                  |   40066 |
| Occitanie                   |  893235 |
| Mayotte                     |   10236 |
| Auvergne-Rh├┤ne-Alpes        | 1139487 |
| ├Äle-de-France               | 1487040 |
| Provence-Alpes-C├┤te d'Azur  |  823968 |
| Centre-Val de Loire         |  351105 |
| Corse                       |   67780 |
| Bourgogne-Franche-Comt├®     |  452564 |
| Normandie                   |  521581 |
| Hauts-de-France             |  902772 |

**Quelle requête SQL utiliser pour afficher le nombre au cumulé de vaccination première dose pour la
 région avec le code 93 uniquement pour le mois de mars 2021 ?**
 
```
 SELECT r.name, sum(n_dose1) AS TOTAL FROM lpecom_covid c INNER JOIN lpecom_regions r ON c.id_region = r.code WHERE r.code= 93 AND jour LIKE '2021-03%';
```

| name                        | TOTAL  |
:----------------------------:|:-------:
| Provence-Alpes-C├┤te d'Azur  | 485530 |

**Quelle requête SQL utiliser pour afficher le record de vaccination première dose en une seule
 journée ? 
Avec une deuxième requête, afficher les informations du département concerné, dont son nom, ainsi
 que le jour du record**
```
SELECT MAX(n_dose1) AS RECCORD_VACCIN FROM lpecom_covid_vaccin;
```

| RECCORD_VACCIN |
:----------------:
|          13511 |

```
SELECT r.*, jour, SUM(n_dose1)
    -> FROM lpecom_covid c
    -> INNER JOIN lpecom_regions r ON c.id_region=r.code GROUP BY jour, id_region
    -> ORDER BY SUM(n_dose1) DESC LIMIT 1;
```
+----+------+----------------+---------------+------------+--------------+
| id | code | name           | slug          | jour       | SUM(n_dose1) |
:---:|:----:|:--------------:|:-------------:|:----------:|:-------------:
|  6 | 11   | ├Äle-de-France  | ile de france | 2021-03-26 |        56661 |


