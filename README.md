# Three-Tier-Distributed-Web-Based-Application

**Overview**

This project is a three-tier distributed web-based application utilizing servlets and JSP technology running on an Apache Tomcat container. The backend is powered by a MySQL database, which maintains a suppliers/parts/jobs/shipments schema. The application provides authentication via a credentials database and supports multiple user roles with distinct permissions.

**Objectives**

* Implement a three-tier web application using JSP, Servlets, JDBC, and MySQL.  
* Utilize user authentication and role-based access.  
* Allow SQL command execution for specific user roles.  
* Enforce referential integrity in MySQL via foreign key constraints.  
* Implement business logic at the application server level, not within MySQL triggers.  

**System Architecture**

The application follows a three-tier architecture:  
* Presentation Layer (Frontend): HTML login page and JSP-based interfaces.  
* Application Layer (Middle Tier): Java servlets handling authentication, SQL execution, and business logic.  
* Data Layer (Backend): MySQL database storing user credentials and project data.  

**Database Schema**

The backend database consists of four tables:  

* suppliers (snum, sname, status, city)  
* parts (pnum, pname, color, weight, city)  
* jobs (jnum, jname, numworkers, city)  
* shipments (snum, pnum, jnum, quantity)  

  * Primary key: (snum, pnum, jnum)  
  * Foreign keys referencing suppliers, parts, and jobs  

A separate credentialsDB manages user authentication.  

**User Roles & Functionalities**

System-Level Application: Handles authentication by validating users against credentialsDB.    

* Root-Level User:   
  *  Executes any SQL query (SELECT, INSERT, UPDATE, DELETE, REPLACE)  
  *  Implements business logic that increments supplier status for high-quantity shipments  

* Client-Level User:  
  *  Executes only SELECT queries on the project4 database  

* Accountant-Level User:  
  *  Cannot execute SQL commands directly  
  *  Runs predefined reports via stored procedures using the CallableStatement interface  

**Setup Instructions**

1. Run the database creation scripts in the following order:  

* mysql -u root -p < project4DBscript.sql  
* mysql -u root -p < credentialsDBscript.sql  
* mysql -u root -p < ClientCreationPermissionsScript.sql  

2. Configure the four properties files for database access:

* Root user  
* Client user  
* Accountant user  
* System-level authentication user  

3. Deploy the web application on Apache Tomcat.  
4. Configure web.xml to map servlets correctly.  
5. Start Tomcat and access the application via a web browser.  
