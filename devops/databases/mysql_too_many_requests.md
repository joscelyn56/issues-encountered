# MySQL Too Many Requests Issue

The amount of connections going to the database at a time becomes too much because the application connection to the
database is more than the database can handle.

## Issue

This happened after I increased the number of simultaneous connections to 50 for a database with spec of
1GB Ram, 1 vCPU and 15GB disk size

## Fix

I upgraded the database spec to 2GB Ram, 1vCPU and 25GB disk
