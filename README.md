# Magento 2 docker

## Introduction

Fork of https://github.com/pgoca/magento2docker

1. Changed Apache to nginx.
2. docker-compose is in version 3.
3. http://localhost:8080 is default address - port may be changed during installation. 
4. Copy database sql file to `db` folder. Installer will ask for full name only.
5. Default path for project files is /var/www/m2/. You can change this in build/docker-compose.yml line 15 `projectAbsolutePath`

## Preparation - best practice 

1. Copy db sql dump to `./db`. Script will select the newest one from this directory.
2. Prepare git link to repo 

## Initialize

1. Run `./bin/build` and follow script instructions
2. Run `./bin/install`

## Scripts

For now there's only one helper script - `./bin/exec`. It will help you with executing commands inside of container.

Usage:
```
./bin/exec <container_suffix> <optional_command>
```

Container suffixes are: php, nginx and db.
If you don't pass an <optional_command>, then it will call `/bin/bash` by default and you'll end up inside of the container.
