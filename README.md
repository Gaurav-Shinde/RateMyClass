# RateMyClass - A place to leave Temple course reviews

![RateMyClass](https://github.com/RateMyClassTU/RateMyClass/blob/main/assets/img/brand/RateMyClassLogo.png?raw=true)

## Description
Rate My Class is a dynamic website for Temple students to view and post reviews for classes in different departments.

## Note
The professors selection, unlike classes, does not have their names; instead, a professor must be added by the user to leave reviews.

## Pre-requisites
Before we begin, you'll need to setup a few things. You'll need
- MySQL Database
- Email for PHP Mailer
- PyMySQL (python package)

## MySQL Script
To use our code, make sure your database doesn't contain the table "Users". Next, take a look at the code below. In the first line, replace the *your database* with the name of the database you'll be using. Then, you will be able to create the table on your database.

### Users
```
CREATE TABLE `*your database*`.`Users` (
  `ID` INT NOT NULL AUTO_INCREMENT,
  `FirstName` VARCHAR(45) NOT NULL,
  `LastName` VARCHAR(45) NOT NULL,
  `Email` VARCHAR(45) NOT NULL,
  `Password` VARCHAR(64) NULL,
  `Acode` VARCHAR(45) NULL,
  `Rdatetime` DATETIME NULL,
  `Adatetime` DATETIME NULL,
  `Status` INT NULL DEFAULT 0,
  `LIdatetime` DATETIME NULL,
  `LOdatetime` DATETIME NULL,
  `Reported` INT NULL DEFAULT 0,
  PRIMARY KEY (`ID`),
  UNIQUE INDEX `ID_UNIQUE` (`ID` ASC),
  UNIQUE INDEX `Email_UNIQUE` (`Email` ASC)
);
```
### Reviews
```
CREATE TABLE `*your database*`.`CourseReviews` (
  `ID` INT NOT NULL AUTO_INCREMENT,
  `Course` VARCHAR(128) NOT NULL,
  `Username` VARCHAR(45) NOT NULL,
  `Comment` VARCHAR(512) NOT NULL,
  `Upvotes` INT NOT NULL DEFAULT 0,
  `Downvotes` INT NOT NULL DEFAULT 0,
  PRIMARY KEY (`ID`),
  UNIQUE INDEX `ID_UNIQUE` (`ID` ASC)
);
```
```
CREATE TABLE `*your database*`.`ProfessorReviews` (
  `ID` INT NOT NULL AUTO_INCREMENT,
  `Professor` VARCHAR(45) NOT NULL,
  `Comment` VARCHAR(512) NOT NULL,
  `Username` VARCHAR(45) NOT NULL,
  `Upvotes` INT NOT NULL DEFAULT 0,
  `Downvotes` INT NOT NULL DEFAULT 0,
  `CourseCode` VARCHAR(45) NOT NULL,
  PRIMARY KEY(`ID`),
  UNIQUE INDEX `ID_UNIQUE` (`ID` ASC)
);
```

### Courses
```
CREATE TABLE `*your database*`.`BulletinGrad` (
  `ID` INT NOT NULL AUTO_INCREMENT,
  `College` VARCHAR(256) NULL,
  `Department` VARCHAR(256) NULL,
  `Course` VARCHAR(256) NULL,
  `Description` VARCHAR(1024) NULL,
  PRIMARY KEY(`ID`),
  UNIQUE INDEX `ID_UNIQUE` (`ID` ASC))
);
```
```
CREATE TABLE `*your database*`.`BulletinUndergrad` (
  `ID` INT NOT NULL AUTO_INCREMENT,
  `College` VARCHAR(256) NULL,
  `Department` VARCHAR(256) NULL,
  `Course` VARCHAR(256) NULL,
  `Description` VARCHAR(1024) NULL,
  PRIMARY KEY(`ID`),
  UNIQUE INDEX `ID_UNIQUE` (`ID` ASC)
);
```
```
CREATE TABLE `*your database*`.`AddedCourses` (
  `ID` INT NOT NULL AUTO_INCREMENT,
  `Course` VARCHAR(256) NULL,
  `Description` VARCHAR(1024) NULL,
  `Username` VARCHAR(45) NULL,
  `Udatetime` DATETIME NULL,
  PRIMARY KEY(`ID`),
  UNIQUE INDEX `ID_UNIQUE` (`ID` ASC)
);
```
### Professors
```
CREATE TABLE `*your database*`.`AddedProfessors` (
  `ID` INT NOT NULL AUTO_INCREMENT,
  `Professor` VARCHAR(128) NOT NULL,
  `Username` VARCHAR(45) NULL,
  `Udatetime` DATETIME NULL,
  PRIMARY KEY (`ID`),
  UNIQUE INDEX `ID_UNIQUE` (`ID` ASC)
);
```

### Reports
```
CREATE TABLE `*your database`.`Reports` (
  `ID` INT NOT NULL AUTO_INCREMENT,
  `Username` VARCHAR(45) NOT NULL,
  `RUsername` VARCHAR(45) NOT NULL,
  `Comment` VARCHAR(512) NULL,
  `Rdatetime` DATETIME NULL,
  PRIMARY KEY (`ID`),
  UNIQUE INDEX `ID_UNIQUE` (`ID` ASC)
);
```

## Server setup
In addition to setting up the MySQL table, you'll also need to setup your server files. This can be found in `assets/php/config.php`. You will have to provide your server credentials to access the MySQL database. You need to do this so that the code is able to access the MySQL tables to do various functions. Examples:
- Authenticating users
- Getting a users rating

## PyMySQL
[PyMySQL](https://pypi.org/project/PyMySQL/) is a python package that helps communicate with MySQL. In order to download it, you'll need a python version of 2.7.x and >= 3.5. To check your version, run `python --version` in your terminal. If you do not have the necessary version of python, you can download it [here](https://www.python.org/downloads/).

Please run the command for your version of python in the console:
#### Python 2.7.x
`pip install PyMySQL`

#### Python >= 3.5
`python3 -m pip install PyMySQL`

## Authentication
For authentication, we used a package, [PHPMailer](https://github.com/PHPMailer/PHPMailer), to allow PHP to send an email to users. In order to do this, you need a email that has low security that you will use for mailing. When you have an email that can use PHPMailer, you'll need edit in your email login and password for:
- register2.php
- reset2.php

## How to run?
Running this project is simple. First, you need to down this project. After using your text editor of choice and configuring some files, you simply upload the files to your web server. Next, you need to make your account an admin by following the next step.

## Managing the server
Every server needs someone to manage it. To start, you need to establish someone as an admin. This can be done by logging into the MySQL database and running the query:
`UPDATE Users SET Status=2 WHERE Email='*your login email*';`

## Recap
Again, you need to edit some files to make it work for you. These are:
  - MySQL scripts must all be edited to work with your database
  - config.php must be edited with your MySQL server information
  - register2.php and reset2.php must be changed with your PHPMailer information (to send verification emails)
  

## Permissions and Restrictions of use 
This repo may be cloned and its code may be used, however credit must be given to Gaurav Shinde and Robert Ni for any modifications or use of the files and code in this repo.  
