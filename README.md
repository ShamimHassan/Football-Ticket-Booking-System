# Football Ticket Booking System - Database Design & SQL Queries

## Project Overview

This project contains the database schema and SQL queries for a Football Ticket Booking System. The system is designed to handle user management, match information, and ticket bookings with proper relational integrity.

## Project Objective

The primary objective of this project is to design and implement a relational database for a Football Ticket Booking System that:

1. **Manage User Accounts**: Maintain user profiles with roles (Football Fan and Ticket Manager) with secure and unique user identifiers
2. **Track Football Match Management**: Store and manage football match information including fixtures, tournament categories, ticket pricing, and real-time availability statuses
3. **Ticket Booking System**: Enable users to book tickets for matches with seat assignments, track payment statuses, and calculate total booking costs
4. **Data Integrity**: Enforce referential integrity through primary and foreign key constraints to maintain data consistency
5. **Query Capabilities**: Provide comprehensive SQL queries to support business operations including match discovery, user search, booking tracking, and analytical reporting

## Database Schema

### 1. Users Table
Stores system users (Football Fans and Ticket Managers)
- `user_id` - Unique identifier (SERIAL PRIMARY KEY)
- `full_name` - User's full name
- `email` - Unique email address
- `role` - User role (Ticket Manager or Football Fan)
- `phone_number` - Optional phone number

### 2. Matches Table
Stores football match information
- `match_id` - Unique match identifier (SERIAL PRIMARY KEY)
- `fixture` - Match teams (e.g., "Real Madrid vs Barcelona")
- `tournament_category` - Tournament type (e.g., Champions League, Premier League)
- `base_ticket_price` - Base ticket price in decimal format
- `match_status` - Current status (Available, Selling Fast, Sold Out, Postponed)

### 3. Bookings Table
Stores ticket booking records
- `booking_id` - Unique booking identifier (SERIAL PRIMARY KEY)
- `user_id` - Foreign key to Users table
- `match_id` - Foreign key to Matches table
- `seat_number` - Optional seat assignment
- `payment_status` - Payment state (Pending, Confirmed, Cancelled, Refunded)
- `total_cost` - Total booking cost

## SQL Queries

The project includes 7 predefined queries:

1. **Upcoming Champions League Matches** - Retrieves available Champions League matches
2. **User Search** - Finds users by name (case-insensitive)
3. **Missing Payment Status** - Identifies bookings with no payment status
4. **Booking Details** - Shows comprehensive booking info with user and match data
5. **All Users & Bookings** - Lists all users including those without bookings
6. **Above Average Bookings** - Finds bookings more expensive than the average
7. **Top 2 Expensive Matches** - Returns the 2nd and 3rd most expensive matches

