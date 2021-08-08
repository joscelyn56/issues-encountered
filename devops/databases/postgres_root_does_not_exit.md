# Postgres Root Does Not Exist

Trying to access the root user on postgres database immediately after installation.

## Problem

After installation, Postgres uses the system name as default user, trying to access the database with
root user throws an error because the root user does not exist.

## Fix
Access the postgres database from the command line using the command below
```bash
psql -U {System Name} -d postgres --no-password
```

Once you have access to the postgres databases, Create a new root user by running the command below on
the postgres console
```bash
CREATE USER root;
```

The new root user has been created, you can access postgres using the root user.
