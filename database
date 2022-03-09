-- CS4400: Introduction to Database Systems (Fall 2021)
-- Phase II: Create Table & Insert Statements [v0] Thursday, October 14, 2021 @ 
-- 2:00pm EDT
-- Team 43
-- Team Member Name (cwilson345)
-- Team Member Name (esinha6)
-- Team Member Name (rponnada3)
-- Team Member Name (avirani32)
-- Directions:
-- Please follow all instructions for Phase II as listed on Canvas.
-- Fill in the team number and names and GT usernames for all members above.
-- Create Table statements must be manually written, not taken from an SQL Dump 
-- file.
-- This file must run without error for credit.

DROP DATABASE IF EXISTS travel_service;
CREATE DATABASE IF NOT EXISTS travel_service;
USE travel_service;

-- ------------------------------------------------------
-- CREATE TABLE STATEMENTS AND INSERT STATEMENTS BELOW
-- ------------------------------------------------------

-- account
DROP TABLE IF EXISTS account;
CREATE TABLE account (
	acctEmail varchar(50) NOT NULL,
	fname varchar(50) NOT NULL,
	lname varchar(50) NOT NULL,
	password varchar(100) NOT NULL,
	PRIMARY KEY (acctEmail)
) ENGINE = InnoDB;

INSERT INTO account VALUES
('mmoss1@travelagency.com', 'Mark', 'Moss', 'password1'),
('asmith@travelagency.com', 'Aviva', 'Smith', 'password2'),
('mscott22@gmail.com', 'Michael', 'Scott', 'password3'),
('arthurread@gmail.com', 'Arthur', 'Read', 'password4'),
('jwayne@gmail.com', 'John', 'Wayne', 'password5'),
('gburdell3@gmail.com', 'George', 'Burdell', 'password6'),
('mj23@gmail.com', 'Michael', 'Jordan', 'password7'),
('lebron6@gmail.com', 'Lebron', 'James', 'password8'),
('msmith5@gmail.com', 'Michael', 'Smith', 'password9'),
('ellie2@gmail.com', 'Ellie', 'Johnson', 'password10'),
('scooper3@gmail.com', 'Sheldon', 'Cooper', 'password11'),
('mgeller5@gmail.com', 'Monica', 'Geller', 'password12'),
('cbing10@gmail.com', 'Chandler', 'Bing', 'password13'),
('hwmit@gmail.com', 'Howard', 'Wolowitz', 'password14'),
('swilson@gmail.com', 'Samantha', 'Wilson', 'password16'),
('aray@tiktok.com', 'Addison', 'Ray', 'password17'),
('cdemilio@tiktok.com', 'Charlie', 'Demilio', 'password18'),
('bshelton@gmail.com', 'Blake', 'Shelton', 'password19'),
('lbryan@gmail.com', 'Luke', 'Bryan', 'password20'),
('tswift@gmail.com', 'Taylor', 'Swift', 'password21'),
('jseinfeld@gmail.com', 'Jerry', 'Seinfeld', 'password22'),
('maddiesmith@gmail.com', 'Madison', 'Smith', 'password23'),
('johnthomas@gmail.com', 'John', 'Thomas', 'password24'),
('boblee15@gmail.com', 'Bob', 'Lee', 'password25');

-- admin
DROP TABLE IF EXISTS admin;
CREATE TABLE admin (
	adminEmail varchar(50) NOT NULL,
	PRIMARY KEY (adminEmail),
	CONSTRAINT admin_fk_1 FOREIGN KEY (adminEmail) REFERENCES account (acctEmail)
) ENGINE = InnoDB;

INSERT INTO admin VALUES
('mmoss1@travelagency.com'),
('asmith@travelagency.com');

-- client
DROP TABLE IF EXISTS client;
CREATE TABLE client (
	clientEmail varchar(50) NOT NULL,
	phoneNumber char(12) NOT NULL,
	PRIMARY KEY (clientEmail),
	UNIQUE KEY phoneNumber (phoneNumber),
	CONSTRAINT client_fk_2 FOREIGN KEY (clientEmail) REFERENCES account (acctEmail)
) ENGINE = InnoDB;

INSERT INTO client VALUES
('mscott22@gmail.com', '555-123-4567'),
('arthurread@gmail.com', '555-234-5678'),
('jwayne@gmail.com', '555-345-6789'),
('gburdell3@gmail.com', '555-456-7890'),
('mj23@gmail.com', '555-567-8901'),
('lebron6@gmail.com', '555-678-9012'),
('msmith5@gmail.com', '555-789-0123'),
('ellie2@gmail.com', '555-890-1234'),
('scooper3@gmail.com', '678-123-4567'),
('mgeller5@gmail.com', '678-234-5678'),
('cbing10@gmail.com', '678-345-6789'),
('hwmit@gmail.com', '678-456-7890'),
('swilson@gmail.com', '770-123-4567'),
('aray@tiktok.com', '770-234-5678'),
('cdemilio@tiktok.com', '770-345-6789'),
('bshelton@gmail.com', '770-456-7890'),
('lbryan@gmail.com', '770-567-8901'),
('tswift@gmail.com', '770-678-9012'),
('jseinfeld@gmail.com', '770-789-0123'),
('maddiesmith@gmail.com', '770-890-1234'),
('johnthomas@gmail.com', '404-770-5555'),
('boblee15@gmail.com', '404-678-5555');

-- customer
DROP TABLE IF EXISTS customer;
CREATE TABLE customer (
	custEmail varchar(50) NOT NULL,
	creditCardNumber char(19) NOT NULL,
	phoneNumber char(12) NOT NULL,
	CVV decimal(3, 0) NOT NULL,
	expDate date NOT NULL,
	currentLocation varchar(100),
	PRIMARY KEY (custEmail),
	UNIQUE KEY creditCardNumber (creditCardNumber),
	CONSTRAINT customer_fk_3 FOREIGN KEY (custEmail) REFERENCES client (clientEmail)
) ENGINE = InnoDB;

INSERT INTO customer VALUES
('scooper3@gmail.com', '6518 5559 7446 1663', '678-123-4567', 551, '2024-02-01', ''),
('mgeller5@gmail.com', '2328 5670 4310 1965', '678-234-5678', 644, '2024-03-01', ''),
('cbing10@gmail.com', '8387 9523 9827 9291', '678-345-6789', 201, '2023-02-01', ''),
('hwmit@gmail.com', '6558 8596 9852 5299', '678-456-7890', 102, '2023-04-01', ''),
('swilson@gmail.com', '9383 3212 4198 1836', '770-123-4567', 455, '2022-08-01', ''),
('aray@tiktok.com', '3110 2669 7949 5605', '770-234-5678', 744, '2022-08-01', ''),
('cdemilio@tiktok.com', '2272 3555 4078 4744', '770-345-6789', 606, '2025-02-01', ''),
('bshelton@gmail.com', '9276 7639 7883 4273', '770-456-7890', 862, '2023-09-01', ''),
('lbryan@gmail.com', '4652 3726 8864 3798', '770-567-8901', 258, '2023-05-01', ''),
('tswift@gmail.com', '5478 8420 4436 7471', '770-678-9012', 857, '2024-12-01', ''),
('jseinfeld@gmail.com', '3616 8977 1296 3372', '770-789-0123', 295, '2022-06-01', ''),
('maddiesmith@gmail.com', '9954 5698 6355 6952', '770-890-1234', 794, '2022-07-01', ''),
('johnthomas@gmail.com', '7580 3274 3724 5356', '404-770-5555', 269, '2025-10-01', ''),
('boblee15@gmail.com', '7907 3513 7161 4248', '404-678-5555', 858, '2025-11-01', '');

-- owner
DROP TABLE IF EXISTS owner;
CREATE TABLE owner (
	ownerEmail varchar(50) NOT NULL,
	PRIMARY KEY (ownerEmail),
	CONSTRAINT owner_fk_4 FOREIGN KEY (ownerEmail) REFERENCES client (clientEmail)
) ENGINE = InnoDB;

INSERT INTO owner VALUES
('mscott22@gmail.com'),
('arthurread@gmail.com'),
('jwayne@gmail.com'),
('gburdell3@gmail.com'),
('mj23@gmail.com'),
('lebron6@gmail.com'),
('msmith5@gmail.com'),
('ellie2@gmail.com'),
('scooper3@gmail.com'),
('mgeller5@gmail.com'),
('cbing10@gmail.com'),
('hwmit@gmail.com');


-- airline
DROP TABLE IF EXISTS airline;
CREATE TABLE airline (
	name varchar(50),
	rating decimal (2,1),
	PRIMARY KEY (name)
) ENGINE = InnoDB;

INSERT INTO airline VALUES
('Delta Airlines',4.7),
('Southwest Airlines',4.4),
('American Airlines',4.6),
('United Airlines',4.2),
('JetBlue Airways',3.6),
('Spirit Airlines',3.3),
('WestJet',3.9),
('Interjet',3.7);

-- airport
DROP TABLE IF EXISTS airport; 
CREATE TABLE airport (
	airportID char(3) NOT NULL, 
	name varchar(100) NOT NULL, 
	timeZone char(3),
	street varchar(100) NOT NULL,
	city varchar(50) NOT NULL,
	state char(2) NOT NULL,
	zip decimal(5, 0) NOT NULL,
	PRIMARY KEY (AirportID),
	UNIQUE KEY (street, city, state, zip)
) ENGINE = InnoDB;

INSERT INTO airport VALUES
('ATL','Atlanta Hartsfield Jackson Airport','EST','6000 N Terminal Pkwy','Atlanta','GA',30320),
('JFK','John F Kennedy International Airport','EST','455 Airport Ave','Queens','NY',11430),
('LGA','Laguardia Airport','EST','790 Airport St','Queens','NY',11371),
('LAX','Lost Angeles International Airport','PST','1 World Way','Los Angeles','CA',90045),
('SJC','Norman Y. Mineta San Jose International Airport','PST','1702 Airport Blvd','San Jose','CA',95110),
('ORD',"O'Hare International Airport",'CST',"10000 W O'Hare Ave",'Chicago','IL',60666),
('MIA','Miami International Airport','EST','2100 NW 42nd Ave','Miami','FL',33126),
('DFW','Dallas International Airport','CST','2400 Aviation DR','Dallas','TX',75261);

-- attractions
DROP TABLE IF EXISTS attractions; 
CREATE TABLE attractions (
	airportID varchar(3) NOT NULL,	
attractionName varchar(100) NOT NULL, 
	PRIMARY KEY (airportID, attractionName),
	CONSTRAINT attractions_fk_5 FOREIGN KEY (airportID) REFERENCES airport (airportID)
) ENGINE = InnoDB;

INSERT INTO attractions VALUES
('ATL','The Coke Factory'),
('ATL','The Georgia Aquarium'),
('JFK','The Statue of Liberty'),
('JFK','The Empire State Building'),
('LGA','The Statue of Liberty'),
('LGA','The Empire State Building'),
('LAX','Lost Angeles Lakers Stadium'),
('LAX','Los Angeles Kings Stadium'),
('SJC','Winchester Mystery House'),
('SJC','San Jose Earthquakes Soccer Team'),
('ORD','Chicago Blackhawks Stadium'),
('ORD','Chicago Bulls Stadium'),
('MIA','Crandon Park Beach'),
('MIA','Miami Heat Basketball Stadium'),
('DFW','Texas Longhorns Stadium'),
('DFW','The Original Texas Roadhouse');

-- properties
DROP TABLE IF EXISTS property;
CREATE TABLE property (
	name varchar(200) NOT NULL,	
	ownerEmail varchar(50) NOT NULL,
	description TEXT,
	capacity int,
	costPerNight int,
	street varchar(50) NOT NULL,
	city varchar(50) NOT NULL,
	state varchar(2) NOT NULL,
	zip varchar(5) NOT NULL,
	PRIMARY KEY (name, ownerEmail),
	UNIQUE KEY (street, city, state, zip),
	CONSTRAINT property_fk_6 FOREIGN KEY (ownerEmail) REFERENCES owner (ownerEmail) 
) ENGINE = InnoDB;

INSERT INTO property VALUES
('Atlanta Great Property','scooper3@gmail.com','This is right in the middle of Atlanta near many attractions!',4,600,'2nd St','ATL','GA',30008),
('House near Georgia Tech','gburdell3@gmail.com','Super close to bobby dodde stadium!',3,275,'North Ave','ATL','GA',30008),
('New York City Property','cbing10@gmail.com','A view of the whole city. Great property!',2,750,'123 Main St','NYC','NY',10008),
('Statue of Libery Property','mgeller5@gmail.com','You can see the statue of liberty from the porch',5,1000,'1st St','NYC','NY',10009),
('Los Angeles Property','arthurread@gmail.com','',3,700,'10th St','LA','CA',90008),
('LA Kings House','arthurread@gmail.com','This house is super close to the LA kinds stadium!',4,750,'Kings St','La','CA',90011),
('Beautiful San Jose Mansion','arthurread@gmail.com','Huge house that can sleep 12 people. Totally worth it!',12,900,'Golden Bridge Pkwt','San Jose','CA',90001),
('LA Lakers Property','lebron6@gmail.com','This house is right near the LA lakers stadium. You might even meet Lebron James!',4,850,'Lebron Ave','LA','CA',90011),
('Chicago Blackhawks House','hwmit@gmail.com','This is a great property!',3,775,'Blackhawks St','Chicago','IL',60176),
('Chicago Romantic Getaway','mj23@gmail.com','This is a great property!',2,1050,'23rd Main St','Chicago','IL',60176),
('Beautiful Beach Property','msmith5@gmail.com','You can walk out of the house and be on the beach!',2,975,'456 Beach Ave','Miami','FL',33101),
('Family Beach House','ellie2@gmail.com','You can literally walk onto the beach and see it from the patio!',6,850,'1132 Beach Ave','Miami','FL',33101),
('Texas Roadhouse','mscott22@gmail.com','This property is right in the center of Dallas, Texas!',3,450,'17th Street','Dallas','TX',75043),
('Texas Longhorns House','mscott22@gmail.com','You can walk to the longhorns stadium from here!',10,600,'1125 Longhorns Way','Dallas','TX',75001);

DROP TABLE IF EXISTS amenities;
CREATE TABLE amenities (
propertyName char(100) NOT NULL,
ownerEmail varchar(50) NOT NULL,
amenityName char(100) NOT NULL,
PRIMARY KEY (propertyName, ownerEmail, amenityName),
CONSTRAINT amenities_fk_7 FOREIGN KEY (propertyName, ownerEmail) REFERENCES property (name, ownerEmail) 
) ENGINE = InnoDB;

INSERT INTO amenities VALUES
('Atlanta Great Property','scooper3@gmail.com','A/C & Heating'),
('Atlanta Great Property','scooper3@gmail.com','Pets allowed'),
('Atlanta Great Property','scooper3@gmail.com','Wifi & TV'),
('Atlanta Great Property','scooper3@gmail.com','Washer and Dryer'),
('House near Georgia Tech','gburdell3@gmail.com','Wifi & TV'),
('House near Georgia Tech','gburdell3@gmail.com','Washer and Dryer'),
('House near Georgia Tech','gburdell3@gmail.com','Full Kitchen'),
('New York City Property','cbing10@gmail.com','A/C & Heating'),
('New York City Property','cbing10@gmail.com','Wifi & TV'),
('Statue of Libery Property','mgeller5@gmail.com','A/C & Heating'),
('Statue of Libery Property','mgeller5@gmail.com','Wifi & TV'),
('Los Angeles Property','arthurread@gmail.com','A/C & Heating'),
('Los Angeles Property','arthurread@gmail.com','Pets allowed'),
('Los Angeles Property','arthurread@gmail.com','Wifi & TV'),
('LA Kings House','arthurread@gmail.com','A/C & Heating'),
('LA Kings House','arthurread@gmail.com','Wifi & TV'),
('LA Kings House','arthurread@gmail.com','Washer and Dryer'),
('LA Kings House','arthurread@gmail.com','Full Kitchen'),
('Beautiful San Jose Mansion','arthurread@gmail.com','A/C & Heating'),
('Beautiful San Jose Mansion','arthurread@gmail.com','Pets allowed'),
('Beautiful San Jose Mansion','arthurread@gmail.com','Wifi & TV'),
('Beautiful San Jose Mansion','arthurread@gmail.com','Washer and Dryer'),
('Beautiful San Jose Mansion','arthurread@gmail.com','Full Kitchen'),
('LA Lakers Property','lebron6@gmail.com','A/C & Heating'),
('LA Lakers Property','lebron6@gmail.com','Wifi & TV'),
('LA Lakers Property','lebron6@gmail.com','Washer and Dryer'),
('LA Lakers Property','lebron6@gmail.com','Full Kitchen'),
('Chicago Blackhawks House','hwmit@gmail.com','A/C & Heating'),
('Chicago Blackhawks House','hwmit@gmail.com','Wifi & TV'),
('Chicago Blackhawks House','hwmit@gmail.com','Washer and Dryer'),
('Chicago Blackhawks House','hwmit@gmail.com','Full Kitchen'),
('Chicago Romantic Getaway','mj23@gmail.com','A/C & Heating'),
('Chicago Romantic Getaway','mj23@gmail.com','Wifi & TV'),
('Beautiful Beach Property','msmith5@gmail.com','A/C & Heating'),
('Beautiful Beach Property','msmith5@gmail.com','Wifi & TV'),
('Beautiful Beach Property','msmith5@gmail.com','Washer and Dryer'),
('Family Beach House','ellie2@gmail.com','A/C & Heating'),
('Family Beach House','ellie2@gmail.com','Pets allowed'),
('Family Beach House','ellie2@gmail.com','Wifi & TV'),
('Family Beach House','ellie2@gmail.com','Washer and Dryer'),
('Family Beach House','ellie2@gmail.com','Full Kitchen'),
('Texas Roadhouse','mscott22@gmail.com','A/C & Heating'),
('Texas Roadhouse','mscott22@gmail.com','Pets allowed'),
('Texas Roadhouse','mscott22@gmail.com','Wifi & TV'),
('Texas Roadhouse','mscott22@gmail.com','Washer and Dryer'),
('Texas Longhorns House','mscott22@gmail.com','A/C & Heating'),
('Texas Longhorns House','mscott22@gmail.com','Pets allowed'),
('Texas Longhorns House','mscott22@gmail.com','Wifi & TV'),
('Texas Longhorns House','mscott22@gmail.com','Washer and Dryer'),
('Texas Longhorns House','mscott22@gmail.com','Full Kitchen');

DROP TABLE IF EXISTS isCloseTo;
CREATE TABLE isCloseTo (
name char(100) NOT NULL,
ownerEmail varchar(100) NOT NULL,
airportID char(3) NOT NULL,
distance decimal(2,0) NOT NULL,
PRIMARY KEY (ownerEmail, name, airportID),
CONSTRAINT isCloseTo_fk_8 FOREIGN KEY (ownerEmail, name) REFERENCES property (ownerEmail, name),
CONSTRAINT isCloseTo_fk_9 FOREIGN KEY (airportID) REFERENCES airport (airportID)
) ENGINE = InnoDB;

INSERT INTO isCloseTo VALUES
('Atlanta Great Property','scooper3@gmail.com','ATL',12),
('House near Georgia Tech','gburdell3@gmail.com','ATL',7),
('New York City Property','cbing10@gmail.com','JFK',10),
('Statue of Libery Property','mgeller5@gmail.com','JFK',8),
('New York City Property','cbing10@gmail.com','LGA',25),
('Statue of Libery Property','mgeller5@gmail.com','LGA',19),
('Los Angeles Property','arthurread@gmail.com','LAX',9),
('LA Kings House','arthurread@gmail.com','LAX',12),
('Beautiful San Jose Mansion','arthurread@gmail.com','SJC',8),
('Beautiful San Jose Mansion','arthurread@gmail.com','LAX',30),
('LA Lakers Property','lebron6@gmail.com','LAX',6),
('Chicago Blackhawks House','hwmit@gmail.com','ORD',11),
('Chicago Romantic Getaway','mj23@gmail.com','ORD',13),
('Beautiful Beach Property','msmith5@gmail.com','MIA',21),
('Family Beach House','ellie2@gmail.com','MIA',19),
('Texas Roadhouse','mscott22@gmail.com','DFW',8),
('Texas Longhorns House','mscott22@gmail.com','DFW',17);

DROP TABLE IF EXISTS flight;
CREATE TABLE flight (
	flightNum int(5),
	airlineName varchar(50),
	fromAirportID char(3),
	toAirportID char(3),
	departureTime time,
	arrivalTime time,
	date date,
	costPerSeat decimal,
	capacity smallint,
	PRIMARY KEY (airlineName, flightNum),
	CONSTRAINT flight_fk_10 FOREIGN KEY (airlineName) REFERENCES airline (name),
	CONSTRAINT flight_fk_11 FOREIGN KEY (fromAirportID) REFERENCES airport (airportID),
	CONSTRAINT flight_fk_12 FOREIGN KEY (toAirportID) REFERENCES airport (airportID)
) ENGINE = InnoDB;

INSERT INTO flight VALUES
(1, 'Delta Airlines', 'ATL', 'JFK', '10:00:00', '12:00:00', '2021-10-18', 400, 150 ),
(2, 'Southwest Airlines', 'ORD', 'MIA', '10:30:00', '14:30:00', '2021-10-18', 350, 125 ),
(3, 'American Airlines', 'MIA', 'DFW', '13:00:00', '16:00:00', '2021-10-18', 350, 125 ),
(4, 'United Airlines', 'ATL', 'LGA', '16:30:00', '18:30:00', '2021-10-18', 400, 100 ),			
(5, 'JetBlue Airways', 'LGA', 'ATL', '11:00:00', '13:00:00', '2021-10-19', 400, 130 ),
(6, 'Spirit Airlines', 'SJC', 'ATL', '12:30:00', '21:30:00', '2021-10-19', 650, 140 ),
(7, 'WestJet', 'LGA', 'SJC', '13:00:00', '16:00:00', '2021-10-19', 700, 100 ),
(8, 'Interjet', 'MIA', 'ORD', '19:30:00', '21:30:00', '2021-10-19', 350, 125 ),
(9, 'Delta Airlines', 'JFK', 'ATL', '08:00:00', '10:00:00', '2021-10-20', 375, 150 ),
(10, 'Delta Airlines', 'LAX', 'ATL', '09:15:00', '18:15:00', '2021-10-20', 700, 110 ),
(11, 'Southwest Airlines', 'LAX', 'ORD', '12:07:00', '19:07:00', '2021-10-20', 600, 95 ),
(12, 'United Airlines', 'MIA', 'ATL', '15:35:00', '17:35:00', '2021-10-20', 275, 115 );

DROP TABLE IF EXISTS rates; 
CREATE TABLE rates (
	ownerEmail varchar(50) NOT NULL,
    custEmail varchar(50) NOT NULL,
	score decimal(1, 0) NOT NULL,
	PRIMARY KEY (custEmail, ownerEmail, score),
	CONSTRAINT rates_fk_13 FOREIGN KEY (custEmail) REFERENCES customer (custEmail),
	CONSTRAINT rates_fk_14 FOREIGN KEY (ownerEmail) REFERENCES owner (ownerEmail)
) ENGINE = InnoDB;

INSERT INTO rates VALUES
('gburdell3@gmail.com', 'swilson@gmail.com', 5),
('cbing10@gmail.com', 'aray@tiktok.com', 5),
('mgeller5@gmail.com', 'bshelton@gmail.com', 3),
('arthurread@gmail.com', 'lbryan@gmail.com', 4),
('arthurread@gmail.com', 'tswift@gmail.com', 4),
('lebron6@gmail.com', 'jseinfeld@gmail.com', 1),
('hwmit@gmail.com', 'maddiesmith@gmail.com', 2);

DROP TABLE IF EXISTS isRatedBy;
CREATE TABLE isRatedBy (
	ownerEmail varchar(50) NOT NULL,
    custEmail varchar(50) NOT NULL,
	score decimal(1, 0) NOT NULL,
	PRIMARY KEY (custEmail, ownerEmail, score),
	CONSTRAINT isRatedBy_fk_15 FOREIGN KEY (custEmail) REFERENCES customer (custEmail),
	CONSTRAINT isRatedBy_fk_16 FOREIGN KEY (ownerEmail) REFERENCES owner (ownerEmail)
) ENGINE = InnoDB;

INSERT INTO isRatedBy VALUES
('gburdell3@gmail.com', 'swilson@gmail.com', 5),
('cbing10@gmail.com', 'aray@tiktok.com', 5),
('mgeller5@gmail.com', 'bshelton@gmail.com', 4),
('arthurread@gmail.com', 'lbryan@gmail.com', 4),
('arthurread@gmail.com', 'tswift@gmail.com', 3),
('lebron6@gmail.com', 'jseinfeld@gmail.com', 2),
('hwmit@gmail.com', 'maddiesmith@gmail.com', 5);

DROP TABLE IF EXISTS review;
CREATE TABLE review (
	name char(100) NOT NULL,
	ownerEmail varchar(50) NOT NULL,
	custEmail varchar(50) NOT NULL,
	content text NOT NULL,
	score decimal(1,0) NOT NULL,
	PRIMARY KEY (ownerEmail, custEmail, name, score),
	CONSTRAINT review_fk_17 FOREIGN KEY (ownerEmail, name) REFERENCES property (ownerEmail, name),
    CONSTRAINT review_fk_18 FOREIGN KEY (custEmail) REFERENCES customer (custEmail)
) ENGINE = InnoDB;

INSERT INTO review VALUES
('House near Georgia Tech', 'gburdell3@gmail.com', 'swilson@gmail.com', 'This was so much fun. I went and saw the coke factory, the falcons play, GT play, and the Georgia aquarium. Great time! Would highly recommend!', 5),
('New York City Property', 'cbing10@gmail.com', 'aray@tiktok.com', 'This was the best 5 days ever! I saw so much of NYC!', 5),
('Statue of Libery Property', 'mgeller5@gmail.com', 'bshelton@gmail.com', 'This was truly an excellent experience. I really could see the Statue of Liberty from the property!', 4),
('Los Angeles Property', 'arthurread@gmail.com', 'lbryan@gmail.com', 'I had an excellent time!', 4),
('Beautiful San Jose Mansion', 'arthurread@gmail.com', 'tswift@gmail.com', "We had a great time, but the house wasn’t fully cleaned when we arrived", 3),
('LA Lakers Property', 'lebron6@gmail.com', 'jseinfeld@gmail.com', 'I was disappointed that I did not meet lebron james', 2),
('Chicago Blackhawks House', 'hwmit@gmail.com', 'maddiesmith@gmail.com', 'This was awesome! I met one player on the chicago blackhawks!', 5);


DROP TABLE IF EXISTS reserve;
CREATE TABLE reserve (
	name char(100),
	ownerEmail varchar(50),
	custEmail varchar(50),
	startDate date,
	endDate date,
	numGuests decimal(4,0),
	PRIMARY KEY (custEmail, ownerEmail, name, startDate),
	CONSTRAINT reserve_fk_19 FOREIGN KEY (custEmail) REFERENCES customer (custEmail),
	CONSTRAINT reserve_fk_20 FOREIGN KEY (ownerEmail, name) REFERENCES property (ownerEmail, name)
) ENGINE = InnoDB;

INSERT INTO reserve VALUES
('House Near Georgia Tech', 'gburdell3@gmail.com', 'swilson@gmail.com', '2021-10-19', '2021-10-25', 3), 
('New York City Property', 'cbing10@gmail.com', 'aray@tiktok.com', '2021-10-18', '2021-10-23', 2),
('New York City Property', 'cbing10@gmail.com', 'cdemilio@tiktok.com', '2021-10-24', '2021-10-30', 2),
('Statue of Libery Property', 'mgeller5@gmail.com', 'bshelton@gmail.com', '2021-10-18', '2021-10-22', 4),
('Los Angeles Property', 'arthurread@gmail.com', 'lbryan@gmail.com', '2021-10-19', '2021-10-25', 2),
('Beautiful San Jose Mansion', 'arthurread@gmail.com', 'tswift@gmail.com', '2021-10-19', '2021-10-22', 10),
('LA Lakers Property', 'lebron6@gmail.com', 'jseinfeld@gmail.com', '2021-10-19', '2021-10-24', 4),
('Chicago Blackhawks House', 'hwmit@gmail.com', 'maddiesmith@gmail.com', '2021-10-19', '2021-10-23', 2),
('Chicago Romantic Getaway', 'mj23@gmail.com', 'aray@tiktok.com', '2021-11-01', '2021-11-07', 2),
('Beautiful Beach Property', 'msmith5@gmail.com', 'cbing10@gmail.com', '2021-10-18', '2021-10-25', 2),
('Family Beach House', 'ellie2@gmail.com', 'hwmit@gmail.com', '2021-10-18', '2021-10-28', 5);


DROP TABLE IF EXISTS book; 
CREATE TABLE book (
custEmail varchar(50) NOT NULL,
flightNum int(5) NOT NULL,
airlineName char(50) NOT NULL,
numSeats int(5) NOT NULL, 
PRIMARY KEY (custEmail, flightNum, airlineName),
CONSTRAINT book_fk_21 FOREIGN KEY (custEmail) REFERENCES customer (custEmail),
CONSTRAINT book_fk_22 FOREIGN KEY (airlineName, flightNum) REFERENCES flight (airlineName, flightNum)
) ENGINE = InnoDB;

INSERT INTO book VALUES
('swilson@gmail.com', 5, 'JetBlue Airways', 3),
('aray@tiktok.com', 1, 'Delta Airlines', 2),
('bshelton@gmail.com', 4, 'United Airlines', 4),
('lbryan@gmail.com', 7, 'WestJet', 2),
('tswift@gmail.com', 7, 'WestJet', 2),
('jseinfeld@gmail.com', 7, 'WestJet', 4),
('maddiesmith@gmail.com', 8, 'Interjet', 2),
('cbing10@gmail.com', 2, 'Southwest Airlines', 2),
('hwmit@gmail.com', 2, 'Southwest Airlines', 5);
