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

## Database Design & Business Logic

The system manages football fans purchasing tickets, upcoming tournament matches, and individual ticket booking receipts.

### Business Logic & Schema Architecture

The database schema design handle these real-world scenarios by implementing the following exact table fields and understanding primary keys, foreign keys, and referential integrity constraints.

### 1. Users Table

This table tracks all administrative staff and customers who use the platform.

| **Field Name** | **What the Field Does** |
| --- | --- |
| `user_id` | Unique identification number for each registered user. |
| `full_name` | Stores the first and last name of the user. |
| `email` | Stores the user's mail address used for login. |
| `role` | Defines access permissions (`Ticket Manager` or `Football Fan`). |
| `phone_number` | Stores the contact mobile number of the fan. |

### 2. Matches Table

This table catalogs the tournament events, stadium logistics, and baseline ticket inventory pricing.

| **Field Name** | **What the Field Does** |
| --- | --- |
| `match_id` | Unique identification number for each football match. |
| `fixture` | Tracks the two competing teams (e.g., *Real Madrid vs Barcelona*). |
| `tournament_category` | The league or cup title (e.g., *Champions League*, *Premier League*). |
| `base_ticket_price` | The foundational price for a single standard entry seat. |
| `match_status` | Current ticket availability state (`Available`, `Selling Fast`, `Sold Out`, `Postponed`). |

### 3. Bookings Table

This transactional table records individual ticket purchases by linking users to their chosen matches.

| **Field Name** | **What the Field Does** |
| --- | --- |
| `booking_id` | Unique tracking transaction number for the ticket purchase. |
| `user_id` | Links the booking directly to the user who made the purchase. |
| `match_id` | Links the booking directly to the specific match being attended. |
| `seat_number` | The specific allocated seat identifier in the stadium (e.g., `A-12`). |
| `payment_status` | Tracks financial resolution (`Pending`, `Confirmed`, `Cancelled`, `Refunded`). |
| `total_cost` | The calculated final invoice price based on the base price and seat quantity. |

## Part 1: ERD Design

Design an Entity Relationship Diagram (ERD) for the Football Ticket Booking System.

### Required Tables

This system includes the following tables:

1. Users
2. Matches
3. Bookings

### Relationship Requirements

This system has the following relationships:

- **One to Many:** One User → Many Bookings (A single football fan can buy tickets for multiple matches throughout the season).
- **Many to One:** Many Bookings → One Match (A major derby match can be associated with thousands of individual booking records from different fans).
- **One to One (logical):** Each individual row in the booking table maps exactly one user to one match for that specific reserved seating choice.

### ERD Elements

This ERD include the following elements:

- Primary Keys (PK)
- Foreign Keys (FK)
- Relationship cardinality (e.g., Crow’s Foot notation)
- Status fields (e.g., booking payment status, match ticket status)

### Submission Format

Link to view the ERD:

✅ **[Lucidchart](https://lucid.app/lucidchart/ac11b0f0-1718-4655-833d-ff588fcb777a/view)** 

## Schema & Sample Data 

### 1. Users Table

| **user_id** | **full_name** | **email** | **role** | **phone_number** |
| --- | --- | --- | --- | --- |
| 1 | Tanvir Rahman | tanvir@mail.com | Football Fan | +8801711111111 |
| 2 | Asif Haque | asif@mail.com | Football Fan | +8801722222222 |
| 3 | Sajjad Rahman | sajjad@mail.com | Ticket Manager | +8801733333333 |
| 4 | Jannat Ara | jannat@mail.com | Football Fan | *NULL* |

### 2. Matches Table

| **match_id** | **fixture** | **tournament_category** | **base_ticket_price** | **match_status** |
| --- | --- | --- | --- | --- |
| 101 | Real Madrid vs Barcelona | Champions League | 150 | Available |
| 102 | Man City vs Liverpool | Premier League | 120 | Selling Fast |
| 103 | Bayern Munich vs PSG | Champions League | 130 | Available |
| 104 | AC Milan vs Inter Milan | Serie A | 90 | Sold Out |
| 105 | Juventus vs Roma | Serie A | 80 | Available |

### 3. Bookings Table

| **booking_id** | **user_id** | **match_id** | **seat_number** | **payment_status** | **total_cost** |
| --- | --- | --- | --- | --- | --- |
| 501 | 1 | 101 | A-12 | Confirmed | 150 |
| 502 | 1 | 102 | B-04 | Confirmed | 120 |
| 503 | 2 | 101 | A-13 | Confirmed | 150 |
| 504 | 2 | 101 | *NULL* | *NULL* | 150 |
| 505 | 3 | 102 | C-20 | Pending | 120 |

## Part 2: SQL Queries & Expected Sample Output

## SQL Queries
This project develops complex SQL queries using `JOIN` variants, subqueries, aggregations, pattern matching, null handling, and pagination.

### Query 1: Retrieve all upcoming football matches belonging to the 'Champions League' where the match status is 'Available'.

**Sample Output:**

| **match_id** | **fixture** | **base_ticket_price** |
| --- | --- | --- |
| 101 | Real Madrid vs Barcelona | 150 |
| 103 | Bayern Munich vs PSG | 130 |

### Query 2: Search for all users whose full names start with 'Tanvir' or contain the phrase 'Haque' (case-insensitive).

- **Concepts used:** `LIKE`, `ILIKE`

**Sample Output:**

| **user_id** | **full_name** | **email** |
| --- | --- | --- |
| 1 | Tanvir Rahman | tanvir@mail.com |
| 2 | Asif Haque | asif@mail.com |

### Query 3: Retrieve all booking records where the payment status is missing (`NULL`), replacing the empty result with 'Action Required'.

- **Concepts used:** `IS NULL`, `COALESCE`

**Sample Output:**

| **booking_id** | **user_id** | **match_id** | **systematic_status** |
| --- | --- | --- | --- |
| 504 | 2 | 101 | Action Required |

### Query 4: Retrieve match booking details along with the User's full name and the scheduled Match fixture teams.

- **Concepts used:** `INNER JOIN`

**Sample Output:**

| **booking_id** | **full_name** | **fixture** | **total_cost** |
| --- | --- | --- | --- |
| 501 | Tanvir Rahman | Real Madrid vs Barcelona | 150 |
| 502 | Tanvir Rahman | Man City vs Liverpool | 120 |
| 503 | Asif Haque | Real Madrid vs Barcelona | 150 |
| 504 | Asif Haque | Real Madrid vs Barcelona | 150 |
| 505 | Sajjad Rahman | Man City vs Liverpool | 120 |

### Query 5: Display a comprehensive list of all users and their booking IDs, ensuring that fans who have *never* bought a ticket are still listed.

- **Concepts used:** `LEFT JOIN / Full JOIN`

**Sample Output:**

| **user_id** | **full_name** | **booking_id** |
| --- | --- | --- |
| 1 | Tanvir Rahman | 501 |
| 1 | Tanvir Rahman | 502 |
| 2 | Asif Haque | 503 |
| 2 | Asif Haque | 504 |
| 3 | Sajjad Rahman | 505 |
| 4 | Jannat Ara | *NULL* |

### Query 6: Find all ticket bookings where the total cost is strictly higher than the average cost of all ticket bookings.

**Sample Output:**

| **booking_id** | **match_id** | **total_cost** |
| --- | --- | --- |
| 501 | 101 | 150 |
| 503 | 101 | 150 |
| 504 | 101 | 150 |

### Query 7: Retrieve the top 2 most expensive matches sorted by base ticket price, skipping the absolute highest premium match.

**Sample Output:**

*(Skips Real Madrid vs Barcelona at 150)*

| **match_id** | **fixture** | **base_ticket_price** |
| --- | --- | --- |
| 103 | Bayern Munich vs PSG | 130 |
| 102 | Man City vs Liverpool | 120 |

## Part 3: Theory Questions (Viva Practice - `Answer`)

## Question 1: What role does a Foreign Key play in the Bookings table, and how does it safeguard against entering a ticket sale for a match that doesn't exist?

let's start with foreign keys using our Football Ticket Booking System as an example! First, what's a foreign key in general? Think of it like a "bridge" or "link" between two tables that keeps your data consistent—no more broken connections!

In our Bookings table, we have two foreign keys:
- `user_id` (links to Users.user_id)
- `match_id` (links to Matches.match_id)

Let's focus on the `match_id` foreign key for this question! The Bookings table uses `match_id` to say, "Hey, this booking is for that specific match over in the Matches table." 

Now, how does it stop us from booking a non-existent match? Let's say someone tries to insert a booking with `match_id = 999`, but there's no match 999 in the Matches table. The database will flat-out reject that insert! Why? Because the foreign key constraint enforces "referential integrity"—meaning every value in the foreign key column must already exist in the primary key column of the table it's referencing. 

It's like trying to buy a ticket for a concert that was never scheduled—you just can't do it because the system checks first! This prevents "orphaned records" (bookings that point to nothing) and keeps our database clean and trustworthy.


## Question 2: Why are we unable to use an aggregate function like `COUNT(booking_id)` inside a standard `WHERE` clause to filter match rows? How does `HAVING` solve this?

Let's break this down step by step, and use our booking system to make it relatable! First, let's remember what aggregate functions are: COUNT(), SUM(), AVG(), MAX(), MIN()—they calculate a single value from a group of rows.

Now, why can't we use them in WHERE? Let's think about the order SQL executes queries in—this is key! The order is:
1. FROM (get the tables)
2. WHERE (filter rows *before* grouping)
3. GROUP BY (group the filtered rows)
4. AGGREGATE FUNCTIONS (calculate on each group)
5. HAVING (filter groups *after* aggregation)
6. SELECT (pick what to show)
7. ORDER BY (sort)

So WHERE runs *before* we even do the grouping and aggregation! At that point, COUNT(booking_id) hasn't been calculated yet—there are no groups to count from! It's like trying to grade a test before the students have even written their answers.

For example, if we wanted "matches with more than 2 bookings", we couldn't write:
```sql
-- THIS WILL FAIL!
SELECT match_id, COUNT(booking_id) 
FROM Bookings 
WHERE COUNT(booking_id) > 2 
GROUP BY match_id;
```

That's where HAVING comes in! HAVING runs *after* GROUP BY and aggregation, so it can filter the groups based on the aggregate result. The correct query is:
```sql
SELECT match_id, COUNT(booking_id) 
FROM Bookings 
GROUP BY match_id 
HAVING COUNT(booking_id) > 2;
```

So to recap: WHERE filters individual rows first, HAVING filters groups after aggregation!


## Question 3: If a Primary Key column guarantees that all row entries are completely unique, why does the database system also explicitly forbid it from containing a `NULL` value?

Let's start with what a primary key (PK) is *supposed* to do: its #1 job is to **uniquely identify every single row in a table**—no exceptions! It's like a person's social security number or a player's jersey number in a team—no two are the same, and everyone has one.

Now, why no NULLs? Let's think about what NULL means in SQL: NULL means "unknown" or "missing value"—it's not zero, it's not an empty string, it's just "we don't know what this is". 

If we allowed a primary key to be NULL, we'd have two big problems:
1. **Uniqueness falls apart**: Wait, can two rows both have NULL as their PK? Because NULL isn't equal to anything—not even another NULL! So how do we tell them apart? If two rows have NULL PKs, we can't uniquely identify them anymore, which breaks the whole point of a PK.
2. **Referential integrity breaks**: Remember foreign keys from Question 1? Foreign keys reference primary keys. If a PK could be NULL, what would a foreign key pointing to it even mean? It would be a reference to "unknown", which is useless for linking tables.

Let's use our Users table as an example: user_id is the PK. If we let user_id be NULL, how would we tell apart two users with NULL user_id? How would Bookings.user_id reference them? It just doesn't work! So databases enforce that PKs are both UNIQUE and NOT NULL—no compromises!


## Question 4: Imagine a newly registered fan who hasn't bought any match tickets yet. If you run a `LEFT JOIN` linking the Users table (left) to the Bookings table (right), what will the resulting rows look like for that specific fan?

let's recall what JOINs do first, and specifically LEFT JOIN! First, let's remember our tables:
- Left table = Users (all our users, including new fans)
- Right table = Bookings (all ticket bookings)

A LEFT JOIN says: "Take EVERYTHING from the left table (Users), and match it up with rows from the right table (Bookings) where the join condition is true (user_id matches). If there's no match for a left row, still keep the left row—just fill the right table's columns with NULL!"

Perfect, so let's apply that to our new fan! Let's say we just added Jannat Ara (user_id=4 from our sample data—wait, actually in our sample data Jannat doesn't have any bookings either! Perfect example!). Let's look at Query 5 from QUERY.sql:

```sql
SELECT u.user_id, u.full_name, b.booking_id
FROM Users u
LEFT JOIN Bookings b ON u.user_id = b.user_id;
```

For Jannat (user 4):
- All the Users table columns (user_id, full_name, email, etc.) will show normally: user_id=4, full_name='Jannat Ara'
- All the Bookings table columns (booking_id, match_id, seat_number, etc.) will be NULL! Because she has no bookings, so there's no matching row in Bookings to pull data from.

So the resulting row for that fan will have their user data intact, and all booking-related columns as NULL—easy peasy!


## Question 5: What is the difference between a main query and a subquery? In what scenarios would you choose to use a subquery over a standard `JOIN` operation?

let's define these terms first using plain English and our booking system!

First, a **main query** is the primary, outer query that gets your final result—it's the "main show". A **subquery** (also called an inner query or nested query) is a query *inside* another query—it's like a "mini-query" that runs first, and its result is used by the main query. Subqueries are usually wrapped in parentheses.

Now, let's use an example from our project! Look at Query 6:
```sql
-- Main query
SELECT booking_id, match_id, total_cost
FROM Bookings
WHERE total_cost > (
  -- Subquery!
  SELECT AVG(total_cost) FROM Bookings
);
```
Here, the subquery calculates the average booking cost first, then the main query uses that value to filter bookings above average.

Now, when to use a subquery instead of a JOIN? Let's list common scenarios:

1. **When you need a single value (scalar subquery)**: Like the average cost example above—you just need one number to compare against, which a subquery gives you easily. A JOIN wouldn't make sense here because we're not linking two tables' rows, just using a calculated value.
2. **When you want to filter based on existence (EXISTS subquery)**: For example, "find users who have at least one booking"—using EXISTS with a subquery is often more efficient than a JOIN for this kind of check.
3. **When the logic is simpler/more readable with a subquery**: Sometimes breaking a problem into two steps (subquery first, then main query) is easier to understand than a complex JOIN with multiple conditions.
4. **When you're working with aggregate functions in filtering**: Like Question 2, sometimes a subquery can help you get aggregated values to use in WHERE clauses (before HAVING is needed).

That said, JOINs are great for combining data from multiple tables into one result set—so pick the right tool for the job!