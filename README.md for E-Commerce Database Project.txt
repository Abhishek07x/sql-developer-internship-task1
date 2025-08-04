Project Overview
This project implements a comprehensive database schema for an e-commerce platform using MySQL. The design follows database normalization principles and includes proper relationships, constraints, and performance optimizations.
Domain: E-commerce Platform
Chosen Domain: Online retail/e-commerce system supporting:

Product catalog management
Customer registration and management
Order processing and tracking
Payment processing
Product reviews and ratings
Shopping cart functionality

Database Schema Design
Entities and Relationships
Primary Entities:

Categories - Product categorization
Users - Customer information
Products - Product catalog
Orders - Customer orders
Suppliers - Product vendors
Addresses - Customer addresses (normalized)

Supporting Entities:
7. Order_Items - Order line items (junction table)
8. Product_Images - Product images
9. Shopping_Cart - User cart items
10. Payments - Payment transactions
11. Reviews - Product reviews
Relationship Types
RelationshipTypeDescriptionUsers → AddressesOne-to-ManyOne user can have multiple addressesCategories → ProductsOne-to-ManyOne category contains many productsProducts → Product_ImagesOne-to-ManyOne product can have multiple imagesUsers → OrdersOne-to-ManyOne user can place multiple ordersOrders ↔ ProductsMany-to-ManyOrders contain multiple products (via Order_Items)Users ↔ Products (Reviews)Many-to-ManyUsers can review multiple productsSuppliers → ProductsOne-to-ManyOne supplier can supply multiple productsOrders → PaymentsOne-to-ManyOne order can have multiple payment attempts
Key Features Implemented
1. Normalization (3NF)

First Normal Form (1NF): All attributes contain atomic values
Second Normal Form (2NF): No partial dependencies on composite keys
Third Normal Form (3NF): No transitive dependencies
Addresses normalized into separate table to avoid redundancy

2. Primary and Foreign Keys

Surrogate Keys: Auto-incrementing integer primary keys for all tables
Foreign Key Constraints: Proper referential integrity with CASCADE options
Composite Keys: Available for junction tables (commented as alternative)

3. Data Integrity Constraints

CHECK constraints: Price validation, rating ranges, quantity validation
UNIQUE constraints: Email uniqueness, product codes, order numbers
NOT NULL constraints: Required fields properly marked
ENUM constraints: Status fields with predefined values

4. Performance Optimizations

Strategic Indexing: Indexes on frequently queried columns
Composite Indexes: Multi-column indexes for complex queries
Views: Pre-defined views for common query patterns
Stored Procedures: Reusable database logic

Technical Implementation
Database Engine

Primary: MySQL (default: InnoDB storage engine)
Features Used:

AUTO_INCREMENT for surrogate keys
TIMESTAMP with automatic updates
Foreign key constraints with referential actions
CHECK constraints for data validation



Sample Data
The schema includes sample data for:

5 product categories
3 suppliers
3 sample users
3 sample products

Views Created

product_catalog: Complete product information with category and supplier
order_summary: Order overview with customer and item count

Schema Highlights
Avoiding Data Redundancy

Customer addresses separated into dedicated table
Product images in separate table (multiple images per product)
Order items normalized to handle quantity and pricing separately
Category information centralized and referenced

Surrogate Keys
All tables use auto-incrementing integer surrogate keys as primary keys for:

Better performance than natural keys
Stability when business rules change
Simplified foreign key relationships

Composite Key Example
sql-- Alternative design for order_items (commented in schema)
UNIQUE KEY unique_order_product (order_id, product_id)
Files Included

ecommerce_schema.sql - Complete database schema with:

Table definitions
Relationships and constraints
Sample data
Views and stored procedures
Performance indexes


README.md - This documentation file
ER_Diagram_Description.txt - Detailed ER diagram description

How to Use

Setup Database:
bashmysql -u username -p < ecommerce_schema.sql

Verify Installation:
sqlUSE ecommerce_db;
SHOW TABLES;
DESCRIBE products;

Test with Sample Queries:
sqlSELECT * FROM product_catalog;
SELECT * FROM order_summary;


Interview Questions - Answered

What is normalization?

Process of organizing data to reduce redundancy and improve data integrity
This schema implements 3NF with separated addresses and normalized relationships


Primary vs Foreign Key:

Primary: Uniquely identifies each record (e.g., user_id in users table)
Foreign: References primary key in another table (e.g., user_id in orders table)


What are constraints?

Rules that enforce data integrity (CHECK, NOT NULL, UNIQUE, FOREIGN KEY)
Examples: price > 0, rating between 1-5, unique email addresses


What is a surrogate key?

Artificial key with no business meaning (e.g., auto-incrementing user_id)
Used in all tables for better performance and stability


How to avoid data redundancy?

Normalization, separate tables for related data
Example: addresses table instead of storing address in users table


What is ER diagram?

Visual representation of database structure showing entities and relationships
Helps design and communicate database structure


Types of relationships:

One-to-One, One-to-Many, Many-to-Many
Examples in schema: Users→Orders (1:M), Orders↔Products (M:M)


AUTO_INCREMENT purpose:

Automatically generates unique sequential numbers for primary keys
Used in all primary key columns for surrogate keys


Default storage engine in MySQL:

InnoDB (supports foreign keys, transactions, row-level locking)


What is composite key:

Primary key made of multiple columns
Example: (order_id, product_id) in order_items table



Future Enhancements

Add inventory tracking tables
Implement product variants (size, color combinations)
Add discount and coupon system
Include shipping and logistics tables
Add product recommendation engine tables

Technologies Used

MySQL 8.0+
SQL DDL (Data Definition Language)
Database design principles
ER modeling concepts


Author: Abhishek Tiwari
Date:  04 August 2025
Course: SQL Developer Internship
Task: Database Setup and Schema Design