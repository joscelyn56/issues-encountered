# Ubuntu Apt-Get Update Command Docker Error

The apt-get update command is a command used to set up a linux distribution before installing any package.

## Problem

The apt-get update command keeps returning a hash sum mismatch error on some required packages to be downloaded 
and then the build stops due to the error displaying the error below.

```dotenv
#12 44.96 E: Some index files failed to download. They have been ignored, or old ones used instead.
```

## Fix

I upgraded the ubuntu version from ubuntu:xenial to ubuntu:bionic, and it worked fine.

## Thoughts

While it seemed like the fix worked fine, I think there are other ways of solving this same issue because 
while searching online I came across several solutions of solving same issue but this was what worked for me.
