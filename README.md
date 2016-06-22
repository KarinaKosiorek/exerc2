CREATE DATABASE Test;
USE Test;

CREATE TABLE Country
(
CountryID int NOT NULL,
Name varchar(255) NOT NULL,
PRIMARY KEY (CountryID)
);

CREATE TABLE City
(
CityID int NOT NULL,
CountryID int NOT NULL,
Name varchar(255) NOT NULL,
Population int NOT NULL,
PRIMARY KEY (CityID),
FOREIGN KEY (CountryID) REFERENCES Country(CountryID)
);

CREATE TABLE Building
(
BuildingID int NOT NULL,
CityID int NOT NULL,
Name varchar(255) NOT NULL,
Floors int NOT NULL,
PRIMARY KEY (BuildingID),
FOREIGN KEY (CityID) REFERENCES City(CityID)
);

INSERT INTO Country
VALUES (1, 'Poland');
INSERT INTO Country
VALUES (2, 'Germany');

INSERT INTO City
VALUES (1, 1, 'Warsaw', 100);
INSERT INTO City
VALUES (2, 1, 'Cracow', 1150);
INSERT INTO City
VALUES (3, 2, 'Munich', 200);

INSERT INTO Building
VALUES (1, 1, 'B1', 3);
INSERT INTO Building
VALUES (2, 1, 'B2', 4);
INSERT INTO Building
VALUES (3, 2, 'B3', 1);

1)
SELECT Country.CountryID, Country.Name FROM 
Country
INNER JOIN 
City
ON Country.CountryID = City.CountryID
GROUP BY Country.CountryID
HAVING SUM(City.Population) > 400;

2)
SELECT Country.Name FROM 
Country 
LEFT JOIN 
(SELECT City.CityID, City.CountryID FROM 
City
INNER JOIN
Building
ON City.CityID = Building.CityID) AS CitiesWithBuldings
ON Country.CountryID = CitiesWithBuldings.CountryID
WHERE CityID IS NULL;

