# Symfony Tips and Tricks

## Symfony Installation and configuration

### Symfony Installation
```bash

# For Symfony Website
$ composer create-project symfony/website-skeleton my_projeùct_name

# For Api based  Application,  console, microservice
$ composer create-project symfony/skeleton my_project_name
```

### Configure existing project
```bash
# Download project
$ cd projects/
$ git clone ...

# Configure project
$ cd my-project/
$ composer install
```
### Display information in .env file

```
$ php bin/console about
```

### Run project

```
$ php bin/console server:start
```

