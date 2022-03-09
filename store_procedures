
-- Christian Wilson (cwilson345)
-- Ruhan Ponnada (rponnada3)
-- Arish Virani (avirani32)
-- Eashan Sinha (esinha6)

-- ID: 1a
-- Name: register_customer
drop procedure if exists register_customer;
delimiter //
create procedure register_customer (
    in i_email varchar(50),
    in i_first_name varchar(100),
    in i_last_name varchar(100),
    in i_password varchar(50),
    in i_phone_number char(12),
    in i_cc_number varchar(19),
    in i_cvv char(3),
    in i_exp_date date,
    in i_location varchar(50)
) 
sp_main: BEGIN
if (i_email in (select email from Accounts natural join Clients))
then if i_email not in (select Email from Customer) then
INSERT INTO Customer (Email, CcNumber,Cvv, Exp_Date, Location)
VALUES (i_email, i_cc_number,i_cvv, i_exp_date,i_location); leave sp_main; 
elseif (i_email in (select email from clients where email = i_email)) then leave sp_main; 
elseif (i_cc_number in (select ccnumber from customer where ccnumber = i_cc_number)) then leave sp_main;
elseif (i_phone_number in (select Phone_Number from Clients where phone_number = i_phone_number))
then leave sp_main; end if; end if;

INSERT INTO Accounts (Email, First_Name, Last_Name,Pass)
VALUES (i_email, i_first_name, i_last_name, i_password);

INSERT INTO Clients (Email,Phone_Number)
VALUES (i_email, i_phone_number);

INSERT INTO Customer (Email, CcNumber,Cvv, Exp_Date, Location)
VALUES (i_email, i_cc_number,i_cvv, i_exp_date,i_location);

END //
delimiter ;


-- ID: 1b
-- Name: register_owner
drop procedure if exists register_owner;
delimiter //
create procedure register_owner (
    in i_email varchar(50),
    in i_first_name varchar(100),
    in i_last_name varchar(100),
    in i_password varchar(50),
    in i_phone_number char(12)
) 
sp_main: BEGIN
	if (i_email in (select email from Accounts natural join Clients))
    then if i_email not in (select Email from Owners) then
	INSERT INTO Owners (Email) VALUES (i_email); leave sp_main; 
	elseif (i_email in (select email from clients where email = i_email)) then leave sp_main; 
    elseif (i_phone_number in (select Phone_Number from Clients where phone_number = i_phone_number))
    then leave sp_main; end if; end if;
    
    INSERT INTO Accounts (Email, First_Name, Last_Name,Pass)
	VALUES (i_email, i_first_name, i_last_name, i_password);
    
    INSERT INTO Clients (Email,Phone_Number)
	VALUES (i_email, i_phone_number);
    
	INSERT INTO Owners (Email) VALUES (i_email);
END //
delimiter ;


-- ID: 1c
-- Name: remove_owner
drop procedure if exists remove_owner;
delimiter //
create procedure remove_owner ( 
    in i_owner_email varchar(50)
)
sp_main: BEGIN
if (select count(*) from Property where Owner_Email = i_owner_email) >= 1 then leave sp_main; end if;
DELETE FROM Owners WHERE Email = i_owner_email;
DELETE FROM Owners_Rate_Customers WHERE Owner_Email = i_owner_email;
DELETE FROM Review WHERE Owner_Email = i_owner_email;
if (select count(*) from Customer where Email = i_owner_email) >= 1 then leave sp_main; 
end if;
delete from clients where Email = i_owner_email; 
delete from accounts where Email = i_owner_email; 

END //
delimiter ;


-- ID: 2a
-- Name: schedule_flight
drop procedure if exists schedule_flight;
delimiter //
create procedure schedule_flight (
    in i_flight_num char(5),
    in i_airline_name varchar(50),
    in i_from_airport char(3),
    in i_to_airport char(3),
    in i_departure_time time,
    in i_arrival_time time,
    in i_flight_date date,
    in i_cost decimal(6, 2),
    in i_capacity int,
    in i_current_date date
)
sp_main: begin
-- TODO: Implement your solution here
	if (select Flight_Num, Airline_Name from flight where Flight_Num = i_flight_num
    and Airline_Name = i_airline_name) in (select Flight_Num, Airline_Name from flight)
    then leave sp_main; end if;
    if i_to_airport = i_from_airport then leave sp_main; end if;
    if i_flight_date <= i_current_date then leave sp_main; end if;
    
    insert into flight values (i_flight_num, i_airline_name, i_from_airport, 
    i_to_airport, i_departure_time, i_arrival_time, i_flight_date, i_cost, i_capacity);
end //
delimiter ;

-- call schedule_flight('3', 'Southwest Airlines', 'MIA', 'DFW', '130000', '160000', '2021-10-18', 350, 125, '2021-11-04');
call schedule_flight('3', 'Southwest Airlines', 'MIA', 'DFW', '130000', '160000', '2021-10-18', 350, 125, '2021-10-04');
call schedule_flight( '1', 'Delta Airlines', 'ATL', 'JFK', '100000', '120000', '2021-10-18', 400, 150, '2021-10-04');
call schedule_flight('14', 'Southwest Airlines', 'DFW', 'DFW', '130000', '160000', '2021-10-18', 350, 125, '2021-10-04');

-- ID: 2b
-- Name: remove_flight
drop procedure if exists remove_flight;
delimiter //
create procedure remove_flight ( 
    in i_flight_num char(5),
    in i_airline_name varchar(50),
    in i_current_date date
) 
sp_main: begin
-- TODO: Implement your solution here
	if (select Flight_Date from flight where Flight_Num = i_flight_num 
    and Airline_Name = i_airline_name limit 1) 
    <= i_current_date then leave sp_main; end if;
    delete from book where Flight_Num = i_flight_num and Airline_Name = i_airline_name;
    delete from flight where Flight_Num = i_flight_num and Airline_Name = i_airline_name;
end //
delimiter ;

-- call remove_flight('2', 'Southwest Airlines', '2021-08-01');
-- call remove_flight('1', 'Delta Airlines', '2021-11-01');


-- ID: 3a
-- Name: book_flight
drop procedure if exists book_flight;
delimiter //
create procedure book_flight (
    in i_customer_email varchar(50),
    in i_flight_num char(5),
    in i_airline_name varchar(50),
    in i_num_seats int,
    in i_current_date date
)
sp_main: begin
-- TODO: Implement your solution here
	if i_num_seats > ((select Capacity from flight where i_flight_num = Flight_Num 
    and i_airline_name = Airline_Name) - (select sum(Num_Seats) from book 
    where i_flight_num = Flight_Num and i_airline_name = Airline_Name 
    group by Flight_Num, Airline_Name)) then leave sp_main; end if;
    
    if i_num_seats < (select Num_Seats from book where Customer = i_customer_email 
    and Flight_Num = i_flight_num and Airline_Name = i_airline_name) then leave sp_main; end if;
    
    if (select Flight_Date from flight where Flight_Num = i_flight_num and Airline_Name = i_airline_name) 
    <= i_current_date then leave sp_main; end if;
    
    if 
    (select Customer, Flight_Num, Airline_Name from book where Customer = i_customer_email 
    and Flight_Num = i_flight_num and Airline_Name = i_airline_name) in (select Customer, 
    Flight_Num, Airline_Name from book) 
    then 
	update book set Num_Seats = i_num_seats where Customer = i_customer_email 
    and Flight_Num = i_flight_num and Airline_Name = i_airline_name;
    end if;
    
    if (select Flight_Date from book join flight on book.Flight_Num = flight.Flight_Num and 
    book.Airline_Name = flight.Airline_Name where book.Flight_Num = i_flight_num 
    and book.Airline_Name = i_airline_name limit 1)
    in (select Flight_Date from book join flight on book.Flight_Num = flight.Flight_Num and 
    book.Airline_Name = flight.Airline_Name where Customer = i_customer_email) 
    then leave sp_main; end if;

    insert into book values (i_customer_email, i_flight_num, i_airline_name, i_num_seats, 0);
end //
delimiter ;

-- works 
-- call book_flight('scooper3@gmail.com', '2', 'Southwest Airlines', 115, '2021-10-01');

-- check num seats - too many
-- call book_flight('scooper3@gmail.com', '2', 'Southwest Airlines', 126, '2021-10-01');
-- call book_flight('scooper3@gmail.com', '2', 'Southwest Airlines', 125, '2021-10-01');

-- same date flights
-- call book_flight('scooper3@gmail.com', '1', 'Delta Airlines', 1, '2021-10-01');

-- check date
-- call book_flight('aray@tiktok.com', '7', 'Westjet', 2, '2021-11-01');

-- check unique --> update num seats (higher seats), should work
-- call book_flight('aray@tiktok.com', '12', 'United Airlines', 2, '2021-10-01');
-- call book_flight('aray@tiktok.com', '12', 'United Airlines', 5, '2021-10-01');

-- check unique --> update num seats (same number) should work, no change
-- call book_flight('aray@tiktok.com', '12', 'United Airlines', 5, '2021-10-01');

-- check unique --> update num seats (lower seats) not work
-- call book_flight('aray@tiktok.com', '12', 'United Airlines', 2, '2021-10-01');

-- check cannot update because not enough additional seats
-- call book_flight('aray@tiktok.com', '2', 'Southwest Airlines', 2, '2021-10-01');

-- check canellation then re-book   
-- call book_flight('aray@tiktok.com', '1', 'Delta Airlines', 2, '2021-10-01');

-- ID: 3b
-- Name: cancel_flight_booking
drop procedure if exists cancel_flight_booking;
delimiter //
create procedure cancel_flight_booking ( 
    in i_customer_email varchar(50),
    in i_flight_num char(5),
    in i_airline_name varchar(50),
    in i_current_date date
)
sp_main: begin
-- TODO: Implement your solution here
	if (select Customer, Flight_Num, Airline_Name from book where Customer = i_customer_email 
    and Flight_Num = i_flight_num and Airline_Name = i_airline_name and Was_Cancelled = 0) 
    not in (select Customer, Flight_Num, Airline_Name from book where Was_Cancelled = 0)
    then leave sp_main; end if;
    
    if (select Flight_Date from book join flight on book.Flight_Num = flight.Flight_Num and 
    book.Airline_Name = flight.Airline_Name where Customer = i_customer_email 
    and book.Flight_Num = i_flight_num and book.Airline_Name = i_airline_name) <= i_current_date
    then leave sp_main; end if;
    
    update book set Was_Cancelled = 1 where Customer = i_customer_email 
    and Flight_Num = i_flight_num and Airline_Name = i_airline_name;
end //
delimiter ;

-- call cancel_flight_booking('bshelton@gmail.com', '4', 'United Airlines', '2021-10-01');
-- call cancel_flight_booking('aray@tiktok.com', '1', 'Delta Airlines', '2021-10-01');
-- call cancel_flight_booking('aray@tiktok.com', '2', 'Southwest Airlines', '2021-11-01');


-- ID: 3c
-- Name: view_flight
create or replace view view_flight (
    flight_id,
    flight_date,
    airline,
    destination,
    seat_cost,
    num_empty_seats,
    total_spent
) as
-- TODO: replace this select query with your solution
select flight.Flight_Num, Flight_Date, flight.Airline_Name, To_Airport, Cost, (Capacity - coalesce(Reserved, 0)), truncate(coalesce(Total_Spent, 0), 3)
from flight left join (select Flight_Num, Airline_Name, Reserved
from (select flight.Flight_Num, flight.Airline_Name, Capacity, sum(Num_Seats) as Reserved
from flight join book on book.Flight_Num = flight.Flight_Num and 
book.Airline_Name = flight.Airline_Name where Was_Cancelled = 0 group by flight.Flight_Num, flight.Airline_Name) 
as capacities) as y on flight.Flight_Num = y.Flight_Num and flight.Airline_Name = y.Airline_Name
left join (select Flight_Num, Airline_Name, sum(Money_Spent) as Total_Spent from
(select Flight_Num, Airline_Name, sum(Money_Spent) as Money_Spent from
(select Flight_Num, Airline_Name, (Cost * Num_Seats) as Money_Spent from (select flight.Flight_Num, flight.Airline_Name, Cost, Num_Seats, Was_Cancelled from flight join book on book.Flight_Num = flight.Flight_Num and 
book.Airline_Name = flight.Airline_Name where Was_Cancelled = 0) as a) as b
group by Flight_Num, Airline_Name
union
select Flight_Num, Airline_Name, sum(Money_Spent) as Money_Spent from
(select Flight_Num, Airline_Name, (0.2 * Cost * Num_Seats) as Money_Spent from (select flight.Flight_Num, flight.Airline_Name, Cost, Num_Seats, Was_Cancelled from flight join book on book.Flight_Num = flight.Flight_Num and 
book.Airline_Name = flight.Airline_Name where Was_Cancelled = 1) as c) as d
group by Flight_Num, Airline_Name) as costs
group by Flight_Num, Airline_Name) as z 
on flight.Flight_Num = z.Flight_Num and flight.Airline_Name = z.Airline_Name;

-- ID: 4a
-- Name: add_property
drop procedure if exists add_property;
delimiter //
create procedure add_property (
    in i_property_name varchar(50),
    in i_owner_email varchar(50),
    in i_description varchar(500),
    in i_capacity int,
    in i_cost decimal(6, 2),
    in i_street varchar(50),
    in i_city varchar(50),
    in i_state char(2),
    in i_zip char(5),
    in i_nearest_airport_id char(3),
    in i_dist_to_airport int
) 
sp_main: BEGIN

IF (SELECT COUNT(*) FROM Property WHERE street = i_street AND city = i_city AND state = i_state and zip = i_zip) > 0 
THEN 
LEAVE sp_main; 
END IF;

IF (SELECT COUNT(*) FROM Property WHERE owner_email = i_owner_email AND property_name = i_property_name) > 0 
THEN 
LEAVE sp_main; 
END IF;

INSERT INTO Property VALUES (i_property_name, i_owner_email, i_description, i_capacity, i_cost, i_street, i_city, i_state, i_zip);

IF (SELECT COUNT(*) FROM Airport WHERE Airport_Id = i_nearest_airport_id) = 0 
THEN 
SET i_nearest_airport_id = NULL; 

SET i_dist_to_airport = NULL; 
END IF;

INSERT INTO Is_Close_To VALUES (i_property_name, i_owner_email, i_nearest_airport_id, i_dist_to_airport);

END //
delimiter ;


-- ID: 4b
-- Name: remove_property
drop procedure if exists remove_property;
delimiter //
create procedure remove_property (
    in i_property_name varchar(50),
    in i_owner_email varchar(50),
    in i_current_date date
)
sp_main: BEGIN
#current date 
IF i_current_date >= (SELECT Start_Date FROM Reserve WHERE i_property_name = Property_Name AND i_owner_email = Owner_Email) 
AND 

i_current_date <= (SELECT End_Date FROM Reserve WHERE i_property_name = Property_Name AND i_owner_email = Owner_Email) 
AND 

(SELECT Was_Cancelled FROM Reserve WHERE i_property_name = Property_Name AND i_owner_email = Owner_Email) = 0 
THEN 

LEAVE sp_main; 
END IF;

DELETE FROM Is_Close_To WHERE i_property_name = Property_Name AND i_owner_email = Owner_Email;

DELETE FROM Property WHERE i_property_name = Property_Name AND i_owner_email = Owner_Email;

DELETE FROM Reserve WHERE i_property_name = Property_Name AND i_owner_email = Owner_Email;

DELETE FROM Review WHERE i_property_name = Property_Name AND i_owner_email = Owner_Email;

DELETE FROM Amenity WHERE i_property_name = Property_Name AND i_owner_email = Property_Owner;
END //
delimiter ;


-- ID: 5a
-- Name: reserve_property
drop procedure if exists reserve_property;
delimiter //
create procedure reserve_property (
    in i_property_name varchar(50),
    in i_owner_email varchar(50),
    in i_customer_email varchar(50),
    in i_start_date date,
    in i_end_date date,
    in i_num_guests int,
    in i_current_date date
)
sp_main: begin
-- TODO: Implement your solution here
	select @count_of_days_overlap := count(*)
    from reserve
    where Customer = i_customer_email and ((Start_Date between i_start_date and i_end_date) 
											or (End_Date between i_start_date and i_end_date)
                                            or (Start_Date <= i_start_date and End_Date >= i_end_date));
	select @total_property_capacity := Capacity 
    from Property
    where Property_Name = i_property_name;
    
--     select @total_span_capacity = @total_property_capacity * (i_start_date - i_end_date);
	
    select @total_guests_booked := sum(Num_Guests)
    from Reserve
    where (Property_Name = i_property_name)
		and ((Start_Date <= i_end_date)
        or (End_Date >= i_start_date));

	if (i_start_date > i_current_date)
		and (@count_of_days_overlap = 0)
        and ((@total_property_capacity - ifnull(@total_guests_booked, 0)) >= i_num_guests) then 
		INSERT INTO `travel_reservation_service`.`Reserve`
		(`Property_Name`,
		`Owner_Email`,
		`Customer`,
		`Start_Date`,
		`End_Date`,
		`Num_Guests`,
		`Was_Cancelled`)
		VALUES
		(i_property_name,
		i_owner_email,
		i_customer_email,
		i_start_date,
		i_end_date,
		i_num_guests,
		0);
	else select "Property not available for number of guests requested";
	end if;
end //
delimiter ;


-- ID: 5b
-- Name: cancel_property_reservation
drop procedure if exists cancel_property_reservation;
delimiter //
create procedure cancel_property_reservation (
    in i_property_name varchar(50),
    in i_owner_email varchar(50),
    in i_customer_email varchar(50),
    in i_current_date date
)
sp_main: begin
-- TODO: Implement your solution here
	select @already_reserved_and_not_cancelled := count(*)
    from Reserve
    where Customer = i_customer_email and Property_Name = i_property_name and Was_Cancelled = 0
					and Start_Date >= i_current_date;
	if ifnull(@already_reserved_and_not_cancelled, 0) > 0 then
		UPDATE `travel_reservation_service`.`Reserve`
		SET `Was_Cancelled` = 1
		WHERE `Property_Name` = i_property_name AND `Owner_Email` = i_owner_email AND `Customer` = i_customer_email;
	end if;

end //
delimiter ;


-- ID: 5c
-- Name: customer_review_property
drop procedure if exists customer_review_property;
delimiter //
create procedure customer_review_property (
    in i_property_name varchar(50),
    in i_owner_email varchar(50),
    in i_customer_email varchar(50),
    in i_content varchar(500),
    in i_score int,
    in i_current_date date
)
sp_main: begin
-- TODO: Implement your solution here
	select @customer_stayed := count(1)
    from Reserve
    where Customer = i_customer_email
		and Property_Name = i_property_name
        and Start_Date <= i_current_date
        and was_cancelled = 0;
    
    select @past_reviews := count(1)
    from Review
    where Property_Name = i_property_name and Customer = i_customer_email;

	if (ifnull(@customer_stayed, 0) >= 1 and ifnull(@past_reviews, 0) = 0) then
		INSERT INTO `travel_reservation_service`.`Review`
		(`Property_Name`,
		`Owner_Email`,
		`Customer`,
		`Content`,
		`Score`)
		VALUES
		(i_property_name,
		i_owner_email,
		i_customer_email,
		i_content,
		i_score);
	end if;
end //
delimiter ;


-- ID: 5d
-- Name: view_properties
create or replace view view_properties (
    property_name, 
    average_rating_score, 
    description, 
    address, 
    capacity, 
    cost_per_night
) as
-- TODO: replace this select query with your solution
select p.Property_Name as property_name,
	(select avg(rv.Score)
    from Review as rv
    where rv.Property_Name = p.Property_Name and rv.Owner_Email = p.Owner_Email) as Avg_Score,
    p.Descr as description,
    concat(p.Street, ', ', p.City, ', ', p.State, ', ', p.Zip) as address,
    p.Capacity as capacity,
    p.Cost as cost_per_night
from Property as p;

-- select p.Property_Name as property_name,
-- 	format((select avg(Score) from Review), 2) as average_rating_score, -- over (partition by r.Property_Name)
--     p.Descr as description,
--     concat(p.Street, ', ', p.City, ', ', p.State, ', ', p.Zip) as address,
--     p.Capacity as capacity,
--     p.Cost as cost_per_night
-- from Property as p;

-- select p.Property_Name as property_name,
-- 	avg(r.Score) over (partition by r.Property_Name) as average_rating_score,
--     p.Descr as descr,
--     concat(p.Street, ', ', p.City, ', ', p.State, ', ', p.Zip) as address,
--     p.Capacity as capacity,
--     p.Cost as cost_per_night
-- from Property as p join Review as r on r.Property_Name = p.Property_Name;

-- ID: 5e
-- Name: view_individual_property_reservations
drop procedure if exists view_individual_property_reservations;
delimiter //
create procedure view_individual_property_reservations (
    in i_property_name varchar(50),
    in i_owner_email varchar(50)
)
sp_main: begin
    drop table if exists view_individual_property_reservations;
    create table view_individual_property_reservations (
        property_name varchar(50),
        start_date date,
        end_date date,
        customer_email varchar(50),
        customer_phone_num char(12),
        total_booking_cost decimal(6,2),
        rating_score int,
        review varchar(500)
    );
    -- TODO: replace this select query with your solution
    
    if not exists(select *
					from Property
					where Property_Name = i_property_name)
		or not exists(select *
						from Owners
                        where Email = i_owner_email)
		then leave sp_main;
	end if;
    insert into view_individual_property_reservations (
		property_name,
        start_date,
        end_date,
        customer_email,
        customer_phone_num,
        total_booking_cost,
        rating_score,
        review
	)
    
    select p.Property_Name as property_name,
			r.Start_Date as start_date,
			r.End_Date as end_date,
			c.Email as customer_email,
			c.Phone_Number as customer_phone_num,
			(datediff(r.End_Date, r.Start_Date) + 1) * p.Cost * if(r.Was_Cancelled = 1, 0.2, 1)
            as total_booking_cost,
			rv.Score as rating_score,
			rv.Content as review
	from Reserve as r
		join Property as p on r.Property_Name = p.Property_Name and r.Owner_Email = p.Owner_Email
        join Clients as c on r.Customer = c.Email
        left join Review as rv on
        p.Property_Name = rv.Property_Name and p.Owner_Email = rv.Owner_Email
        and rv.Customer = c.Email
	where r.Property_Name = i_property_name and p.Owner_Email = i_owner_email;
end //
delimiter ;


-- ID: 6a
-- Name: customer_rates_owner
drop procedure if exists customer_rates_owner;
delimiter //
create procedure customer_rates_owner (
    in i_customer_email varchar(50),
    in i_owner_email varchar(50),
    in i_score int,
    in i_current_date date
)
sp_main: BEGIN

IF (SELECT Start_Date FROM Reserve WHERE CONCAT(i_customer_email, i_owner_email) = CONCAT(Customer, Owner_Email)) > i_current_date 
AND

(SELECT Was_Cancelled FROM Reserve WHERE CONCAT(i_customer_email, i_owner_email) = CONCAT(Customer, Owner_Email)) = 1 
OR 

i_customer_email NOT IN (SELECT Email FROM Customer) OR i_owner_email NOT IN (SELECT Email FROM Owners) 
OR 

CONCAT(i_customer_email, i_owner_email) IN (SELECT CONCAT(Customer, Owner_Email) FROM Customers_Rate_Owners) 

THEN LEAVE sp_main; 
END IF;

INSERT INTO Customers_Rate_Owners VALUES(i_customer_email, i_owner_email, i_score);

END //
delimiter ;


-- ID: 6b
-- Name: owner_rates_customer
drop procedure if exists owner_rates_customer;
delimiter //
create procedure owner_rates_customer (
    in i_owner_email varchar(50),
    in i_customer_email varchar(50),
    in i_score int,
    in i_current_date date
)
sp_main: BEGIN

IF (SELECT Start_Date FROM Reserve WHERE CONCAT(i_customer_email, i_owner_email) 

= CONCAT(Customer, Owner_Email)) > i_current_date 
AND 
(SELECT Was_Cancelled FROM Reserve WHERE CONCAT(i_customer_email, i_owner_email) 

= CONCAT(Customer, Owner_Email)) = 1 
OR  
i_customer_email NOT IN (select Email FROM Customer) 

OR 
i_owner_email NOT IN (SELECT Email FROM Owners) 
 
OR 
CONCAT(i_customer_email, i_owner_email) IN (SELECT CONCAT(Customer, Owner_Email) FROM Owners_Rate_Customers)

THEN 
LEAVE sp_main; 
END IF;

INSERT INTO Owners_Rate_Customers VALUES(i_owner_email, i_customer_email, i_score);
END //
delimiter ;


-- ID: 7a
-- Name: view_airports
create or replace view view_airports (
    airport_id, 
    airport_name, 
    time_zone, 
    total_arriving_flights, 
    total_departing_flights, 
    avg_departing_flight_cost
) as
-- TODO: replace this select query with your solution    
SELECT airport_id, airport_name, time_zone, 
IFNULL(Arrivals.arrivals,0), 
IFNULL(Departures.departures,0), 
flight_cost FROM Airport

LEFT JOIN

(SELECT To_Airport, 
COUNT(To_Airport) AS arrivals FROM Flight
GROUP BY To_Airport) 
AS Arrivals ON Airport.airport_id = Arrivals.To_Airport

LEFT JOIN

(SELECT From_Airport, 
COUNT(From_Airport) AS departures, 
AVG(Cost) AS flight_cost FROM Flight
GROUP BY From_Airport) 
AS Departures ON Airport.Airport_Id = Departures.From_Airport;

-- ID: 7b
-- Name: view_airlines
create or replace view view_airlines (
    airline_name, 
    rating, 
    total_flights, 
    min_flight_cost
) as
-- TODO: replace this select query with your solution
SELECT Airline.Airline_Name, Rating, 
COUNT(Flight_Num), 
MIN(Cost) 

	FROM Airline JOIN Flight ON Flight.Airline_Name=Airline.Airline_Name 
    GROUP BY Airline_Name,
    Rating;


-- ID: 8a
-- Name: view_customers
create or replace view view_customers (
    customer_name, 
    avg_rating, 
    location, 
    is_owner, 
    total_seats_purchased
) as
-- TODO: replace this select query with your solution
-- view customers
select concat(First_Name,' ',Last_Name) as customer_name,
avg(o_r_c.score) as avg_rating,(c.Location) as location, 
case when o.Email is not null then 1 else 0 end as is_owner,
ifnull(sum(b.num_seats),0) as total_seats_purchased
FROM customer c left join owners O on C.Email = O.Email
left join book b on c.email = b.customer
left join owners_rate_customers o_r_c on c.email = o_r_c.customer
left join accounts a on c.email = a.Email
group by c.Email;


-- ID: 8b
-- Name: view_owners
create or replace view view_owners (
    owner_name, 
    avg_rating, 
    num_properties_owned, 
    avg_property_rating
) as
-- TODO: replace this select query with your solution
select concat(First_Name,' ',Last_Name) as owner_name, 
avg(c.Score) as avg_rating,
count(distinct p.Property_Name) as num_properties_owned,
avg(rev.score) as avg_property_rating from
owners o left join reserve res on o.email = res.owner_email
left join property p on o.Email = p.owner_email
left join review rev on p.property_name = rev.property_name
left join customers_rate_owners c on res.customer = c.Customer and res.Owner_email = C.Owner_email  
left join accounts a on o.Email = a.Email
group by o.Email;


-- ID: 9a
-- Name: process_date
drop procedure if exists process_date;
delimiter //
create procedure process_date ( 
    in i_current_date date
)
sp_main: BEGIN
	update (book inner join customer on book.customer = customer.email) natural join (flight inner join airport on to_airport = airport_id) set 
    customer.location = airport.state where book.was_cancelled = '0' and flight.flight_date = i_current_date ;
    leave sp_main;
END //
delimiter ;
