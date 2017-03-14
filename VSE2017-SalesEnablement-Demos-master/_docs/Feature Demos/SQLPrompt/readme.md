# SQL Prompt for Visual Studio Enterprise 

## Overview
SQL Prompt for Visual Studio Enterprise is an add-in for Visual Studio that extends and enhances the standard IntelliSense-style code
completion. SQL Prompt can make your developers twice as fast at working with SQL, and leaves them free to concentrate on how the code actually
works.

It helps your team work with each other’s code and write consistent queries.

Using SQL Prompt allows you to improve productivity by stripping away the repetition of coding. As well as making the most common queries,
such as SELECTs and INSERTs, quick to write, SQL Prompt completes JOIN conditions for you automatically. You don't have to remember any column
names or aliases.

## Demo Script

*Let’s connect to a database from the Server Explorer window in Visual Studio* *and take a look at some of the highlights*

**Section A**
  -   Create a connection to the PartsUnlimited database
  -   Open a new query – right click ‘new query’

  *Our database has an orders table, lets imagine we want to improve the functionality around retrieving order details.*
  
  *First let’s take a look at Orders, not only does SQL Prompt autocomplete database and object names but it also completes T-SQL commands like SELECT.*

  ````NOTE: If you don’t see a prompt – hit the spacebar!````

**Section B**
  1. Type ‘SE’ complete to SELECT
  2. Type ‘\* F’ complete to FROM
  3. Select Order

  ***As you can see it also qualifies and uses square brackets where necessary***

  4. Go – Execute query
````SQL
  --Code completions for T-SQL Commands
    SELECT \* FROM dbo.\[Order\]
````
  ***In addition to this it also works with Keywords, lets create a stored procedure to retrieve all Orders***

**Section C: Creating Stored Procedures**

1. Type ‘CR’ complete to CREATE

2. Type ‘PRO’ complete to PROCEDURE

3. Type ‘GetOrders A’ complete to AS

4. Type ‘BE’ complete to BEGIN

5. Repeat Section B1-3 to add select statement

6. Type ‘E’ complete to END

7. Go – Execute query

````SQL
--Code completion of keywords

CREATE PROCEDURE GetOrders AS
BEGIN
SELECT \* FROM dbo.\[Order\]
END
GO
````
  ***It’s easy for us to work with ‘SELECT \*’ but really we want to be specific about the columns we are selecting, with SQL Prompt we canexpand wildcard with our completion key.***

**Section D: Expanding Wildcard Characters**

1. Place cursor to the right of ‘\*’ in existing SELECT statement

2. Press ‘Tab’ to expand

3. Highlight ‘CREATE’

4. Type ‘AL’ complete to ALTER

5. Execute Query

````SQL
--Expansion of Wildcard
ALTER PROCEDURE GetOrders AS
BEGIN
SELECT \[Order\].OrderId ,
       \[Order\].Address ,
       \[Order\].City ,
       \[Order\].Country ,
       \[Order\].Email ,
       \[Order\].FirstName ,
       \[Order\].LastName ,
       \[Order\].OrderDate ,
       \[Order\].Phone ,
       \[Order\].PostalCode ,
       \[Order\].State ,
       \[Order\].Total ,
       \[Order\].Username FROM dbo.\[Order\]
END
GO
````
***What if we wanted to connect this information to our User information? As well as mid-string matching, SQL Prompt also allows CamelCase suggestions***

**Section E: Finding a table name**

1. Repeat B1-2

2. Type ‘NU’ complete AspNetUsers from CamelCase matches

3. Go – Execute Query


````SQL
--CamelCase 'I know I want a User table but what is it called'

SELECT \* FROM dbo.AspNetUsers -- Use nu

GO
````

*There is no foreign key relationship to Order here but SQL Prompt will still suggest a join condition based upon the matching column names*

** Section F: Adding Join Conditions **

-   F1. Repeat B1-3

-   F2. Type ‘JO’ complete JOIN

-   F3. Type ‘NU’ complete AspNetUsers

-   F4. Type ‘ON ’ complete suggested join on UserName

-   F5. Go – Execute Query

````SQL
--Join conditions without foreign keys

SELECT \* FROM dbo.\[Order\] JOIN dbo.AspNetUsers ON AspNetUsers.UserName = \[Order\].Username

GO
````
*Let’s wrap this up in a stored procure to retrieve details of a specific order and user*

**Section G**

1. Type ‘CR’ complete to CREATE

2. Type ‘PRO’ complete to PROCEDURE

3. Type ‘GetOrder @ID A’ complete to AS

4. Type ‘BE’ complete to BEGIN

5. Repeat Section F1-4 to add select statement

6. Type ‘WH’ complete to WHERE

7. Type ‘ ‘ select OrderID

8. Type ‘@’ complete to @ID

9. Type ‘E’ complete to END

10. Optionally expand the wildcard again

10. Go – Execute query

````SQL
--Code highlighting + maybe column picker??

CREATE PROCEDURE GetOrder @ID INT AS
BEGIN

SELECT \* FROM dbo.\[Order\] JOIN dbo.AspNetUsers ON
AspNetUsers.UserName = \[Order\].Username 
WHERE \[Order\].OrderId = @ID

END
GO
````
***Next let’s add a new order record to check we can retrieve it - SQL Prompt autocompletes insert statements with column lists for us
too***

**Section H: Autocomplete Insert Statements**

1. Type ‘IN’ complete to INSERT

2. Type ‘INT’ complete to INTO

3. Select Order complete to full column list

4. Update the VALUES with some made up data (N’Made up data’)

5. Ensure the UserName value is N’Administrator@test.com’

6. Go - Execute Query

````SQL
--Insert statements completing with column list

INSERT INTO dbo.\[Order\]
        ( Address ,
          City ,
          Country ,
          Email ,
          FirstName ,
          LastName ,
          OrderDate ,
          Phone ,
          PostalCode ,
          State ,
          Total ,
          Username)

VALUES  ( N'123 Some Street' , -- Address - nvarchar(max)
          N'Seattle' , -- City - nvarchar(max)
          N'USA' , -- Country - nvarchar(max)
          N'admin@test.com' , -- Email - nvarchar(max)
          N'Tom' , -- FirstName - nvarchar(max)
          N'Austin' , -- LastName - nvarchar(max)
          SYSDATETIME() , -- OrderDate - datetime2
          N'5551235897' , -- Phone - nvarchar(max)
          N'99999' , -- PostalCode - nvarchar(max)
          N'WA' , -- State - nvarchar(max)
          39.99 , -- Total - decimal
          N'Administrator@test.com'  -- Username - nvarchar(max)
        )
````
***Let’s check it is in the Table***

**Section I**
1. Repeat B1-4

2. Note the OrderID from the results

````SQL
SELECT \* FROM dbo.\[Order\]
````
*And now lets test our stored procedure, when writing EXEC statements SQL Prompt even include a parameter list for us:*

**Section J**

1. Type ‘EX’ complete to EXEC

2. Select ‘GetOrder’

3. Edit the value to match the OrderID from I2.

4. Execute Query

````SQL
--Auto-complete EXEC statements with parameter lists

EXEC dbo.GetOrder @ID = 2 -- int
````

## Summary
There’s a quick tour of the highlights of SQL Prompt Free Edition. It’s available in Visual Studio Enterprise 2017 and it improves your productivity by speeding up SQL development tasks and reducing risk of error, so you can get back to the task in hand.  