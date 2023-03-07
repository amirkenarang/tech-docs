# PostgreSQL

## ****How to Install and Setup PostgreSQL server on Ubuntu****

First, you should install prerequisite software packages that will be used to download and install software certificates for a secure SSL connection.

`sudo apt install wget ca-certificates`

Then, get the certificate, add it to apt-key management utility and create a new configuration file with an official PostgreSQL repository address inside.

```bash
# Create the file repository configuration:
sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'

# Import the repository signing key:
wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -

# Update the package lists:
sudo apt-get update

# Install the latest version of PostgreSQL.
# If you want a specific version, use 'postgresql-12' or similar instead of 'postgresql':
sudo apt-get -y install postgresql

# To install another version:
sudo apt-get -y install postgresql-14
```

****Check PostgreSQL status****

After the installation, you may double-check that the PostgreSQL daemon is active.

`service postgresql status`

![Untitled](PostgreSQL%20236110bd1f234692ae94d8deb8c29120/Untitled.png)

### **Start Using the PostgreSQL Command Line Tool**

When you install PostgreSQL a default admin user `postgres` is created by the default. You must use it to log in to your PostgreSQL database for the first time.

A `psql` command-line client tool is used to interact with the database engine. You should invoke it as a `postgres` user to start an interactive session with your local database.

`sudo -u postgres psql`

In addition to creating a postgres admin user for you, PostgreSQL installation also creates a default database named `postgres` and connects you to it automatically when you first launch `psql`.

After first launching `psql`, you may check the details of your connection by typing `\conninfo` into the interpreter.

![Untitled](PostgreSQL%20236110bd1f234692ae94d8deb8c29120/Untitled%201.png)

You are now connected to the database `postgres` as a user `postgres`.

### **Create and Populate a New Database**

You are now connected to your database server through psql command line tool with full access rights, so it’s time to create a new database.

`CREATE DATABASE <db-name>;`

After the new `<db-name>` database is created, connect to it.

`\c <db-name>`

Now you are ready to start creating tables where your data will be stored. Let’s create your first table with a primary key, and three client attributes.

`CREATE TABLE clients (id SERIAL PRIMARY KEY, first_name VARCHAR, last_name VARCHAR, role VARCHAR);`

You may double-check that your new table is created successfully by typing a `\dt` command.

Let’s now insert the first row into your newly created `clients` table.

`INSERT INTO clients (first_name, last_name, role) VALUES ('John', 'Smith', 'CEO');`

And query the table to get all its rows.

`SELECT * FROM clients;`

![Untitled](PostgreSQL%20236110bd1f234692ae94d8deb8c29120/Untitled%202.png)

## **Setup PostgreSQL server**

It’s fun to play with the database locally, but eventually, you will need to connect to it through a remote server.

<aside>
💡 When you install a PostgreSQL server, *it is only accessible locally through the loopback IP address of your machine*. However, you may change this setting in the PostgreSQL configuration file to allow remote access.

</aside>

Let’s now exit the interactive psql session by typing `exit` and accessing `postgresql.conf` configuration file of PostgreSQL version 14 by using the nano text editor.

`sudo nano /etc/postgresql/14/main/postgresql.conf`

Uncomment and edit the `listen_addresses` attribute to start listening to start listening to all available IP addresses.

`listen_addresses = '*'`

![Untitled](PostgreSQL%20236110bd1f234692ae94d8deb8c29120/Untitled%203.png)

Now edit the PostgreSQL access policy configuration file.

`sudo nano /etc/postgresql/14/main/pg_hba.conf`

Append a new connection policy (a pattern stands for `[CONNECTION_TYPE][DATABASE][USER] [ADDRESS][METHOD]`) at the bottom of the file.

`host all all 0.0.0.0/0 md5`

![Untitled](PostgreSQL%20236110bd1f234692ae94d8deb8c29120/Untitled%204.png)

We are allowing TCP/IP connections (`host`) to all databases (`all`) for all users (`all`) with any IPv4 address (`0.0.0.0/0`) using an MD5 encrypted password for authentication (`md5`).

It is now time to restart your PostgreSQL service to load your configuration changes.

`systemctl restart postgresql`

And make sure your system is listening to the 5432 port that is reserved for PostgreSQL.

`ss -nlt | grep 5432`

If everything is OK, you should see this output

## Important Queries:

- **Get Database list:**

`\l`

If you want to see a list of all the databases that are available on a server, use the `\l` command.

![Untitled](PostgreSQL%20236110bd1f234692ae94d8deb8c29120/Untitled%205.png)

- **Create User:**

`CREATE USER <username>;`

- **Change Password:**

Since the default `postgres` user does not have a password, you should set it yourself.

`\password <username>`

- **Create Database:**

`CREATE DATABASE <db-name>;`

- **Get User List:**

`\du`

And to see a list of all the users with their privileges use the `\du` command.

![Untitled](PostgreSQL%20236110bd1f234692ae94d8deb8c29120/Untitled%206.png)

- **Create Table**

`CREATE TABLE clients (id SERIAL PRIMARY KEY, first_name VARCHAR, last_name VARCHAR, role VARCHAR);`

- **Drop Database:**

`DROP DATABASE <database name>;`

# Remove PostgreSQL:

Run this command:

```bash
sudo apt-get --purge remove postgresql postgresql-*
```