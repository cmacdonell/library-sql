---
layout: lesson
root: .
title: Databases using SQL
minutes: 60
---

## Setup

_Note: this should have been done by participants before the start of the workshop._

1. Install [Firefox](https://www.mozilla.org/en-US/firefox/new/)
2. Install the SQLite Manager add on: **Menu (the three horizontal lines near the
top right corner of Firefox) -> Add-ons -> Search -> SQLite
Manager -> Install -> Restart now**
4. Add SQLite Manager to the menu: **Menu -> Customize, then drag the SQLite
   Manager icon to one of the empty menu squares on the right, Exit Customize**
5. Open SQLite Manager: **Menu -> SQLite Manager**

## What is SQL?

SQL (Structured Query Language) is a powerful language used to interrogate and manipulate relational databases.
It is highly specialised. It is not a general programming language that you can use to write an entire program.
However, SQL queries can be embedded in other programming languages to let any program work with databases.
There are several different kinds of SQL, but all support the same basic statements that we will be covering today.

## Relational databases

Relational databases consist of one or more tables of data. These tables have _fields_ (columns) and _records_ (rows).
Every field has a data _type_. Every value in the same field of each record has the same _type_. These tables can be
linked to each when a field in one table can be matched to a field in another table. SQL _queries_ are the commands
that let you look up data in a database or make calculations based on columns.

## Why use SQL

Using SQL lets you keep the data separate from the analysis. There is no risk of accidentally changing data when
you are analysing it. If the data is changed, a saved query can be re-run to analyse the new data.

SQL is optimised for handling large amounts of data. Using data types helps with quality control of entries - you
will receive an error if you try to enter a word into a field that should contain a number. Understanding the nature
of relational databases, and using SQL, will help you in using databases in programming languages.
to do similar things using programming languages such as R or Python.

## Why are Librarians well suited to SQL?
Librarianship is about information management. We help sort and organise information and we help people find information. Most of us use mediated queries to help people find the information they need e.g. conducting a search via a library catalogue. With SQL, you can directly construct your database queries without the constraints (e.g. field name or search limitations) imposed by a mediated search interface. Librarians are good at searching information so don’t be afraid – constructing queries using SQL is simply a different and more direct way of finding information. 

## Database Management Systems

There are a number of different database management systems for working with
relational data. We're going to use SQLite today, but basically everything we
teach you will apply to the other database systems as well (e.g., MySQL,
PostgreSQL, MS Access, Filemaker Pro). The only things that will differ are the
details of exactly how to import and export data and the
[details of data types](#datatypediffs).


## Database Design

* Every row-column combination contains a single *atomic* value, i.e., not
   containing parts we might want to work with separately.
* One field per type of information
* No redundant information
    * Split into separate tables with one table per class of information
    * Needs an identifier in common between tables – shared column - to
       reconnect (foreign key).


## Introduction to SQLite Manager

Let's all open the database we downloaded in SQLite Manager by clicking on the
open file icon.

You can see the tables in the database by looking at the left hand side of the
screen under Tables.

To see the contents of a table, click on that table and then click on the Browse
and search tab in the right hand section of the screen.

If we want to write a query, we click on the Execute SQL tab.


## Dataset Description

The data we will be using is a time-series for a small mammal community in
southern Arizona. This is part of a project studying the effects of rodents and
ants on the plant community that has been running for almost 40 years.  The
rodents are sampled on a series of 24 plots, with different experimental
manipulations controlling which rodents are allowed to access which plots.

This is a real dataset that has been used in over 100 publications. We've
simplified it just a little bit for the workshop, but you can download the
[full dataset](http://esapubs.org/archive/ecol/E090/118/) and work with it using
exactly the same tools we'll learn about today.


## Import

1. Download the three CSV files from the [Portal Database](http://figshare.com/articles/Portal_Project_Teaching_Database/1314459)
1. Start a New Database **Database -> New Database**
2. Start the import **Database -> Import**
3. Select the file to import
4. Give the table a name that matches the file name (surveys, species, plots), or use the default
5. If the first row has column headings, check the appropriate box
6. Make sure the delimiter and quotation options are appropriate for the CSV files.  Ensure 'Ignore trailing Separator/Delimiter' is left *unchecked*.
7. Press **OK**
8. When asked if you want to modify the table, click **OK**
9. Set the data types for each field: choose TEXT for fields with text
   (`species_id`, `genus`, `sex`, etc.) and INT for fields with numbers (`day`,
   `month`, `year`, `weight`, etc.)

> ### Challenge
>
> Import the plots and species tables

You can also use this same approach to append new data to an existing table.


## Adding data to existing tables

1. Browse & Search -> Add
1. Enter data into a csv file and append


## <a name="datatypes"></a> Data types

| Data type                          | Description                                                                                              |
|------------------------------------|:---------------------------------------------------------------------------------------------------------|
| CHARACTER(n)                       | Character string. Fixed-length n                                                                         |
| VARCHAR(n) or CHARACTER VARYING(n) | Character string. Variable length. Maximum length n                                                      |
| BINARY(n)                          | Binary string. Fixed-length n                                                                            |
| BOOLEAN                            | Stores TRUE or FALSE values                                                                              |
| VARBINARY(n) or BINARY VARYING(n)  | Binary string. Variable length. Maximum length n                                                         |
| INTEGER(p)                         | Integer numerical (no decimal).                                                                          |
| SMALLINT                           | Integer numerical (no decimal).                                                                          |
| INTEGER                            | Integer numerical (no decimal).                                                                          |
| BIGINT                             | Integer numerical (no decimal).                                                                          |
| DECIMAL(p,s)                       | Exact numerical, precision p, scale s.                                                                   |
| NUMERIC(p,s)                       | Exact numerical, precision p, scale s. (Same as DECIMAL)                                                 |
| FLOAT(p)                           | Approximate numerical, mantissa precision p. A floating number in base 10 exponential notation.          |
| REAL                               | Approximate numerical                                                                                    |
| FLOAT                              | Approximate numerical                                                                                    |
| DOUBLE PRECISION                   | Approximate numerical                                                                                    |
| DATE                               | Stores year, month, and day values                                                                       |
| TIME                               | Stores hour, minute, and second values                                                                   |
| TIMESTAMP                          | Stores year, month, day, hour, minute, and second values                                                 |
| INTERVAL                           | Composed of a number of integer fields, representing a period of time, depending on the type of interval |
| ARRAY                              | A set-length and ordered collection of elements                                                          |
| MULTISET                           | A variable-length and unordered collection of elements                                                   |
| XML                                | Stores XML data                                                                                          |


## <a name="datatypediffs"></a> SQL Data Type Quick Reference

Different databases offer different choices for the data type definition.

The following table shows some of the common names of data types between the various database platforms:

| Data type                                               | Access                    | SQLServer            | Oracle             | MySQL          | PostgreSQL    |
|:--------------------------------------------------------|:--------------------------|:---------------------|:-------------------|:---------------|:--------------|
| boolean                                                 | Yes/No                    | Bit                  | Byte               | N/A            | Boolean       |
| integer                                                 | Number (integer)          | Int                  | Number             | Int / Integer  | Int / Integer |
| float                                                   | Number (single)           | Float / Real         | Number             | Float          | Numeric       |
| currency                                                | Currency                  | Money                | N/A                | N/A            | Money         |
| string (fixed)                                          | N/A                       | Char                 | Char               | Char           | Char          |
| string (variable)                                       | Text (<256) / Memo (65k+) | Varchar              | Varchar / Varchar2 | Varchar        | Varchar       |
| binary object	OLE Object Memo	Binary (fixed up to 8K)   | Varbinary (<8K)           | Image (<2GB)	Long | Raw	Blob          | Text	Binary | Varbinary     |

Previous: [Index](index.html) Next: [Basic queries.](01-sql-basic-queries.html)
