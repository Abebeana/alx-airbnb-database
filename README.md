# Airbnb-like Database Schema

## Overview

This project contains the SQL schema and sample data for a simplified Airbnb-style booking system. It includes tables for Users, Properties, Bookings, Payments, Reviews, Messages, and Locations.

## Features

- **Users:** Guests, Hosts, and Admin roles.
- **Properties:** Listings linked to hosts, with detailed location info.
- **Bookings:** Reservations by users with status tracking.
- **Payments:** Payments linked to bookings with multiple payment methods.
- **Reviews:** User ratings and comments on properties.
- **Messages:** Communication between users.
- **Locations:** Separate table to avoid location redundancy (3NF compliance).

## Database Normalization

- The schema is normalized up to **Third Normal Form (3NF)**.
- Location data is extracted into its own table to reduce redundancy.
- Calculated fields like total booking price should be handled carefully.

## How to Use

1. Run the `CREATE TABLE` scripts to set up the database schema.
2. Insert sample data using the provided SQL insert statements.
3. Extend and adapt the schema as needed for your application.

## Notes

- This schema is designed for **PostgreSQL**; minor adjustments may be required for other SQL databases.
- UUIDs are used as primary keys for uniqueness.
- Enum fields are implemented using `VARCHAR` with `CHECK` constraints.

---

Feel free to reach out if you want help with schema modifications, data generation, or queries!

