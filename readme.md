# Synchronized Databases

A mini-project that [Ahmed Grati](https://github.com/AhmedGrati) and I worked on during our __Distributed Systems__ workshop at INSAT.

## Problem:

Obviously, there are tons of different ways to synchronize distributed databases. 
<br>

Let's imagine that we have an unusual situation with restrictions below: 

* A future system will have some Head Office (HO) and a couple of Branch Offices (BOs). 
* All offices are located in different places, and some of them have limitation with the internet connection. 

It could even be a situation where the internet is available for 1-2 hours per day. 
<br>

The perfect solution is to write your own DB sync mechanism data between branches using **RabbitMQ Message queues**. 
<br>

For this lab we assume one *Head Office (HO)* and *3 Branch offices (BO)* for sales. The 3 sales branches are physically separated from the Head office. They manage their databases independently and they need to synchronise their data to the Head office that maintain the hole data of sales. We assume that the database are based on the **product sales** table with the following structure.

| Date | Region | Product | Qty | Cost | Amt | Tax | Total |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 2021-04-29 | East | Paper | 73 | 12.95 | 945.35 | 66.17 | 1,011.52 |
| 2021-04-29 | West | Paper | 33 | 12.95 | 427.35 | 29.91 | 457.26 |
| 2021-04-30 | East | Pens | 14 | 2.19 | 30.66 | 2.15 | 32.81 |
| 2021-04-30 | West | Pens | 40 | 2.19 | 87.60 | 6.13 | 93.73 |
| 2021-05-01 | East | Paper | 21 | 12.95 | 271.95 | 19.04 | 290.99 |
| 2021-05-01 | West | Paper | 10 | 12.95 | 129.50 | 9.07 | 138.57 |

The main of this lab is to create a distributed application that synchronisation databases from the product sales tables. This application needs to use the __RabbitMQ__ to send data on the related queues. We run 3 distributed processes that synchronise data from the first BO to HO, the second BO to the HO and the third BO to HO. For this lab we use Java with JDBC connector for __PostgreSQL__ databases for sales. So, 4 databases are needed for the 3 BO and one HO. *The synchronisation is made by the 3 BO.*

## Project's design:

<p align="center">
  <img src="https://github.com/hajali-amine/synchronized-databases/blob/main/assets/App_design.png" alt="design" />
</p>

## Requirements:

* RabbitMQ (using the port 5672).
* PostgreSQL (using the port 5432).
* Create the Databases __bo1__, __bo2__, __bo3__ and __ho__.

## Process:

1. Execute the SQL files in the *ho* and the *bo* packages in the database.
2. Execute HoJob: *java HoJob*
3. Execute BoJob with an argument of 1: *java BoJob 1*
4. Execute BoJob with an argument of 2: *java BoJob 2*
5. Execute BoJob with an argument of 3: *java BoJob 3*

## Have fun!