---
title: "Working with SQL Server in Docker"
summary: "Guide to get you started with SQL Server using Docker."
date: 2021-07-01
draft: false
---

## Introduction
Working with SQL Server in Docker have several benfits. It's extremely fast to get up and running, we basically type one command with some environment variables and we are up and running. It's cross-plattform, so doesn't matter if your team mates are working in Linux, MacOS, Windows or any other OS. We can skip writing a long step-by-step readme of how to setup the server by providing a Dockerfile. If we want to create some integrationtests we can spin up a SQL Server run tests against it and tear it down in matter of seconds, why not go further and automate the process in our CI/CD workflow? And this is just to mention a few.

In this article we will start with exploring the basics; how to get SQL Server running in Docker. You will learn how to create and connect to a database, create a table and insert some data into it and then get a vizualization of the values inside the table. Everything will be done manually through the CLI.

## Docker
First off we need a SQL Server running in Docker for our project. We can do this with one line, so type the following command into your terminal to run the mssql container.
```bash
docker run -d --name my-test-container -e 'ACCEPT_EULA=Y' -e 'SA_PASSWORD=AsomewhatSTRONGpw10€' -p 1433:1433 mcr.microsoft.com/mssql/server:latest
```

### Breaking down the command we just ran:
Detached mode or `-d`, lets us run our container in the background. 

`--name my-test-container` is the name of the container, feel free to change `my-test-container` with your name of choice if you want.

With `-e` we can set local environment variables. 
* Setting `'ACCEPT_EULA=Y'` variable to `Y` to confirm our acceptance of the End-User Licensing Agreement. This is required setting for the SQL Server image.
* We also need to set a password for the system administrator user `sa`, and we do this by adding `'SA_PASSWORD=AsomewhatSTRONGpw10€'`, you can change `AsomewhatSTRONGpw10€` with a strong password of your choice as well. 

`-p` is specifying the port we are going to use, in our case `1433:1433` which is commonly used for a SQL Database engine.

The last parameter we us is the Docker image `mcr.microsoft.com/mssql/server:latest`, if you desire a different version you can find what versions are available (here)[https://hub.docker.com/_/microsoft-mssql-server]

## Testing the mssql container manually
To test the container we can create a database and table manually through the CLI. To run an interactive bash shell inside our **my-test-container** container we run `sudo docker exec -it my-test-container "bash"` in the terminal. `-it` is `-i` and `-t` combined, more about what they mean can be found [here](https://docs.docker.com/engine/reference/commandline/exec/).

When we have a shell inside the container we can connect to the **sqlcmd** by running this command: `/opt/mssql-tools/bin/sqlcmd -S localhost -U sa -P "AsomewhatSTRONGpw10€"`. Now we can start typing some SQL commands.

Let's create the database:
```sql
CREATE DATABASE TestDB
GO
```
The CREATE command is not executed by default, therefore we type `GO` on the new line to execute the previous commands.

And to use the newly created database run:
```sql
USE TestDB
GO
```

Now we want to create a table, to create "Beverages" with two types of drinks inside it we can run the following. Notice that we first create the table, the insert two beverages and then run `GO`. So you don't need to run `GO` after every single command by itself, you can use it to combine a chain of commands and run `GO` after as well.
```sql
CREATE TABLE Beverages (id INT, name NVARCHAR(50), stock INT)
INSERT INTO Beverages VALUES (1, 'Zingo', 200); INSERT INTO Beverages VALUES (2, 'Trocadero', 30)
GO
```

To see what when have created in our database we run a select command:
```sql
SELECT * FROM Beverages
GO
```

And then we should get a neat visualization of our table.
```
id          name                                               stock
----------- -------------------------------------------------- -----------
          1 Zingo                                                      200
          2 Trocadero                                                   30
```

To exit the CLI just type `exit` and press enter.