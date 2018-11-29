# Mocker - Magento 2 docker 

## Introduction

Version 1.0 of Mocker

## Preparation  

Edit `build\custom.conf`

1. Change `projectAbsolutePath` to Your all projects folder. 
2. Copy db sql dump to `./db`. Script will select the newest one from this directory.
3. Prepare git link to repo.
4. You can enter gitRepoLink in `build\custom.conf` but You will be asked in building step anyway.   

## Building

1. Run `./bin/build` and follow script instructions. 

    Docker will prepare necessary files. If You want add additional Magento, files copy them to `./magento` folder after the build step. Otherwise they will be overwritten.
    
    During installation You will be asked to enter:
    
    * Git repository URL - this is optional but makes all much easier. Note that when project folder is not empty git will skip downloading files.
    * Project source folder - it's Your project folder like `0000-Magento`. You should change absolute path in `build\custom.conf`
    * Project name - based on that variable program will create docker containers
    * Project number - it's crucial. Base on that program will create ports for docker.
    * PHP version - Magento 2 supports PHP 7.0 and 7.1 but You can choose any other.
    * Database name - it's database name inside container. You may leave it default.
    
    You will be asked:
    
    ``` Do you want to import newest database dump from db directory (e - enter filename)? [Y/n/e] ```
    
    Y (default) - Program will search for **newest** sql file in `./db` and prepare installation file to import it.
    n - program will skip this step. You can import db any time inside db container
    e - You can enter db name of Your choose (file must be present in db folder.) format: `filename.sql`  


## Installation

1. Run `./bin/install`

This may take a while. Especially if You are running docker for the first time. 

## Scripts

Each build is prepared for one project. After installation You will need at least.   

* ```./docker-compose.yml``` 
* `./bin` folder.

For now there's only one helper script - `./bin/exec`. It will help you with executing commands inside of container.

Usage:
```
./bin/exec <container_suffix> <optional_command>
```
Eg.

```
bin/exec node "npm -v"
```

Container suffixes are: php, nginx, db and node.
If you don't pass an <optional_command>, then it will call `/bin/bash` by default and you'll end up inside of the container.

During building process program will copy `.build/php_bashrc` to `./php`. This file contains aliases. You can use them only inside php container. 
``` bin/exec php ```. 


By deafult Mailhog is running at port 6025.  6XXX where XXX are 3 last digits of Your project. 

There is no need to keep all containers running. Eg. after system restart dockers will stop. To restart them enter:

``` bin/start ``` 


## Fork differences and useful informations

Fork of https://github.com/pgoca/magento2docker

1. Changed Apache to nginx.
2. docker-compose is in version 3.
3. http://localhost:8080 is default address - port may be changed during installation. 
4. Copy database sql file to `db` folder. Installer will choose to newset one from the folder. You can also type database of Your choice.
5. Default path for project files is /var/www/m2/. You can change this in bin/custom.conf `projectAbsolutePath`. You can also change this path during installation.