# Database driver not found

Laravel uses php mysql driver behind the scene to handle database connections and requests.

## Problem

Laravel 8.12 started throwing a php error out of the blue. After investigation, I realized php docker 
installation set for php 7.4 was using php 8.1 cli so laravel was throwing error due to the discrepancy.

## Fix

I updated laravel/framework to the latest version and also update the php version in my docker file to php 8.1.
