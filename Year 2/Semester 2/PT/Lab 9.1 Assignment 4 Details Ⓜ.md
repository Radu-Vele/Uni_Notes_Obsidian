---
tags: [Notebooks/PT]
title: Lab 9.1 Assignment 4 Details Ⓜ
created: '2022-04-21T07:13:33.864Z'
modified: '2022-05-18T19:12:36.055Z'
---

# Lab 9.1 Assignment 4 Details :m:

## Brief
- food delivery management system with account option

### Users
1. Administrator :white_check_mark:
  - import initial products from .csv :white_check_mark:
  - add/delete/modify products :white_check_mark:
  - create combinations of products (e.g. daily menu) => product :white_check_mark:
  - generate reports about performed orders:
    - time interval (orders between x and y hours) :white_check_mark:
    - products ordered more than a number of times :white_check_mark:
    - clients that have ordered more than a certain number of times + value of the order is higher than x. :white_check_mark:
    - products ordered in a specific day and the number of times they've been ordered :white_check_mark:

2. Client :white_check_mark:
  - register with user & passwd :white_check_mark:
  - view product list :white_check_mark:
  - search for products based on keyword/rating/nr of calories/ ... :white_check_mark:
  - create an order of several products + receive bill :white_check_mark:

3. Regular employee :white_check_mark:
- notified when a new order is performend

## Design
- layered architecture
- composite design pattern (Products)
- observer design pattern (Employee notification)
- implement DeliveryService using a HashMap or so

Important Class **Delivery Service**:


## TODO:
- steps defined in the intellij project

## Questions:
- well formed method?
- design by contract?
