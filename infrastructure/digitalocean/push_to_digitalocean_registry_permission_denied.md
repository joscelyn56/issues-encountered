# Push to DigitalOcean Container Registry Permission Denied Error

DO container registry is used to store docker images that can be pulled and run in a container manager.

## Problem

Periodically, attempts to push docker image to digitalocean container registry is returning a permission 
denied error after it each works. It was caused by an issue from DO and can also be caused by a stuck 
garbage collection on the container registry.

## Fix
This was fixed by the DigitalOcean support

## Source
DigitalOcean support
