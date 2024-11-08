-- DROP SCHEMA public;

CREATE SCHEMA public AUTHORIZATION postgres;

COMMENT ON SCHEMA public IS 'standard public schema';
-- public.additional_services definition

-- Drop table

-- DROP TABLE additional_services;

CREATE TABLE additional_services (
	additional_service_id int8 NOT NULL,
	title varchar(100) NOT NULL,
	price float4 NULL,
	description varchar NOT NULL,
	CONSTRAINT additional_services_pk PRIMARY KEY (additional_service_id)
);


-- public.bookings definition

-- Drop table

-- DROP TABLE bookings;

CREATE TABLE bookings (
	booking_id int8 NOT NULL,
	client_id int8 NOT NULL,
	date_start date NOT NULL,
	date_end date NULL,
	room_id int8 NOT NULL,
	CONSTRAINT bookings_pk PRIMARY KEY (booking_id)
);


-- public.clients definition

-- Drop table

-- DROP TABLE clients;

CREATE TABLE clients (
	client_id int8 NOT NULL,
	f varchar(50) NOT NULL,
	o varchar(50) NOT NULL,
	i varchar(50) NULL,
	birth_date date NOT NULL,
	birth_place varchar NOT NULL,
	phone varchar NOT NULL,
	email varchar NOT NULL,
	passport_series varchar(4) NOT NULL,
	passport_number varchar(6) NOT NULL,
	passport_issue_place varchar NOT NULL,
	passport_issue_date date NOT NULL,
	address varchar NOT NULL,
	"password" varchar NOT NULL,
	CONSTRAINT clients_pk PRIMARY KEY (client_id)
);


-- public.equipment definition

-- Drop table

-- DROP TABLE equipment;

CREATE TABLE equipment (
	equipment_id int8 NOT NULL,
	title varchar(100) NOT NULL,
	CONSTRAINT equipment_pk PRIMARY KEY (equipment_id)
);


-- public.floors definition

-- Drop table

-- DROP TABLE floors;

CREATE TABLE floors (
	floor_id int8 NOT NULL,
	title varchar NOT NULL,
	CONSTRAINT floors_pk PRIMARY KEY (floor_id)
);


-- public.housekeepings definition

-- Drop table

-- DROP TABLE housekeepings;

CREATE TABLE housekeepings (
	housekeeping_id int8 NOT NULL,
	employee_id int8 NOT NULL,
	floor_id int8 NOT NULL,
	cleaning_date date NOT NULL,
	CONSTRAINT housekeepings_pk PRIMARY KEY (housekeeping_id)
);


-- public.roles definition

-- Drop table

-- DROP TABLE roles;

CREATE TABLE roles (
	role_id int8 NOT NULL,
	title varchar NOT NULL,
	CONSTRAINT roles_pk PRIMARY KEY (role_id)
);


-- public.room_categories definition

-- Drop table

-- DROP TABLE room_categories;

CREATE TABLE room_categories (
	room_category_id int8 NOT NULL,
	title varchar(100) NOT NULL,
	description varchar NOT NULL,
	price float4 NOT NULL,
	CONSTRAINT room_categories_pk PRIMARY KEY (room_category_id)
);


-- public.room_status definition

-- Drop table

-- DROP TABLE room_status;

CREATE TABLE room_status (
	room_status_id int8 NOT NULL,
	title varchar(20) NOT NULL,
	CONSTRAINT room_status_pk PRIMARY KEY (room_status_id)
);


-- public.rooms definition

-- Drop table

-- DROP TABLE rooms;

CREATE TABLE rooms (
	room_id int8 NOT NULL,
	floor_id int8 NOT NULL,
	"number" int4 NOT NULL,
	room_category_id int8 NOT NULL,
	room_status_id int8 NOT NULL,
	CONSTRAINT rooms_pk PRIMARY KEY (room_id)
);


-- public.rabotniki definition

-- Drop table

-- DROP TABLE rabotniki;

CREATE TABLE rabotniki (
	employee_id int8 NOT NULL,
	f varchar NOT NULL,
	o varchar NOT NULL,
	i varchar NOT NULL,
	employee_category_id int8 NOT NULL,
	phone varchar NOT NULL,
	CONSTRAINT staff_pk PRIMARY KEY (employee_id)
);


-- public.rabotniki_categories definition

-- Drop table

-- DROP TABLE rabotniki_categories;

CREATE TABLE rabotniki_categories (
	employee_category_id int8 NOT NULL,
	title varchar NOT NULL,
	CONSTRAINT staff_categories_pk PRIMARY KEY (employee_category_id)
);


-- public.polsovateli definition

-- Drop table

-- DROP TABLE polsovateli;

CREATE TABLE polsovateli (
	username varchar NOT NULL,
	"password" varchar NOT NULL,
	role_id int8 NOT NULL,
	employee_id int8 NOT NULL,
	CONSTRAINT users_pk PRIMARY KEY (username)
);


-- public.booking_additional_services definition

-- Drop table

-- DROP TABLE booking_additional_services;

CREATE TABLE booking_additional_services (
	booking_id int8 NOT NULL,
	additional_service_id int8 NOT NULL,
	count int4 NOT NULL,
	CONSTRAINT booking_additional_services_pk PRIMARY KEY (booking_id, additional_service_id),
	CONSTRAINT booking_additional_service2s_fk FOREIGN KEY (additional_service_id) REFERENCES additional_services(additional_service_id),
	CONSTRAINT booking_additional_services_fk FOREIGN KEY (booking_id) REFERENCES bookings(booking_id)
);


-- public.room_equipment definition

-- Drop table

-- DROP TABLE room_equipment;

CREATE TABLE room_equipment (
	room_category_id int8 NOT NULL,
	equipment_id int8 NOT NULL,
	CONSTRAINT room_equipment_pk PRIMARY KEY (room_category_id, equipment_id),
	CONSTRAINT room_equipment_fk FOREIGN KEY (room_category_id) REFERENCES room_categories(room_category_id),
	CONSTRAINT room_equipment_fk_1 FOREIGN KEY (equipment_id) REFERENCES equipment(equipment_id)
);
