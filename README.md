# Magento 1 docker

## Initialize

1. Run `./bin/build` and follow script instructions
2. Run `./bin/install`
3. Install script will give you IPs of containers, use it or add them to your /etc/hosts


## Scripts

For now there's only one helper script - `./bin/exec`. It will help you with executing commands inside of container.

Usage:
```
./bin/exec <container_suffix> <optional_command>
```

Container suffixes are: php, apache and db.
If you don't pass an <optional_command>, then it will call `/bin/bash` by default and you'll end up inside of the container.