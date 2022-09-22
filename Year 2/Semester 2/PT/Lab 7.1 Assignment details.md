---
tags: [Notebooks/PT]
title: Lab 7.1 Assignment details
created: '2022-04-02T10:34:57.988Z'
modified: '2022-04-19T20:49:40.234Z'
---

# Lab 7.1 Assignment details

## What our app does?
- is destined for the employees in a warehouse in order:
  - to deal with products to the database (Add, Edit, Remove, View All)
  - add clients to the database (Add, Edit Delete, View all)
  - process orders (that are also stored in a database) (client <-> products + quantity) => impact on the product stock

## About layered architecture
- layer -> certain responsabilities / specific functionalities (independent and isolated ish)
- Communication between layers -> ***REQUESTS*** (unidirectional, only neighbours communicate)


## Model
- fields mapping to the table columns - class called **entity**

## TODO:
- study Layered Design Pattern + Singleton :white_check_mark:
  - compare theory with given example :white_check_mark:
- work on the template presentation :white_check_mark:
- create database tables and link to code :white_check_mark:

1. Deal with operations for ***CLIENT***
1.1. Insert :white_check_mark:
1.2. Edit (search by email address) :white_check_mark:
1.3. Delete :white_check_mark:
1.4. View All (JTable) :white_check_mark:
2. Deal with operations for ***PRODUCT***
2.1. Add new :white_check_mark:
2.2. Edit :white_check_mark:
2.3. Delete :white_check_mark:
2.4. View All :white_check_mark:

> The items in stock must be >= 0. Items with stock = 0 must also be added, but additional checks must be performed when working with the stock to make sure the product is in stock. The stock cannot be decremented below 0.

3. Deal with operations for ***ORDER***
3.1. Select Client :white_check_mark:
3.2. Select Product :white_check_mark:
3.3. Insert into orders :white_check_mark:

4. Reflection method to generate table columns and populate table :white_check_mark:

5. Bill for each order (pdf) :white_check_mark:

6. Generic DAO (dynamically generated queries) * :white_check_mark:

7. JavaDoc :white_check_mark:

8. Documentation

## Questions:
1. Do we need unique fields for product?
