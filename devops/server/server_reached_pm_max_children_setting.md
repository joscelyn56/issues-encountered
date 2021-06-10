# Server Reached pm.max_children Setting

The pm in pm.max_children refers to PHP FPM's Process Manager so, simply put, the pm.max_children setting limits how many
requests can be served by PHP simultaneously.

## Problem

Once the traffic goes high on your website, the rate at which your server responds to request becomes very slow which can cause timeouts.

## Fix

Calculate how many processes your server can run simultaneously using this [PHP-FPM Process Calculator](https://spot13.com/pmcalculator/)
Adjust pm settings to match result of calculation to solve issue.

## Source

[https://chrismoore.ca/2018/10/finding-the-correct-pm-max-children-settings-for-php-fpm/](https://chrismoore.ca/2018/10/finding-the-correct-pm-max-children-settings-for-php-fpm/)
