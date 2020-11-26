# docker-wordpress
Wordpress, PHP-FPM 7.4, MySQL 8, Nginx Setup

# About the repo

It was a mix of things.  I wanted to brush up on my WordPress, as well as learn about Docker.  Hopefully you find this helpful.

# Getting Started
## Prerequisites
- Docker
- Git

## Installation
1. Clone the repo
```bash
git clone https://github.com/danfoust/docker-wordpress.git
```
2. Run docker-compose
```bash
docker-compose up -d
```

## Personalizing
You can personalize this setup by installing git and then updating the WordPress Dockerfile to pull in your theme repository (using git clone).

## Other helpful additions
Copy and paste these commands into your Wordpress Dockerfile to be able to use these packages

### Composer (PHP package manager)
```bash
RUN curl -sS https://getcomposer.org/installer -o composer-setup.php \
  && HASH=`curl -sS https://composer.github.io/installer.sig` \
  && php -r "if (hash_file('SHA384', 'composer-setup.php') === '$HASH') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" \
  && php composer-setup.php --version=1.10.17 --install-dir=/usr/local/bin --filename=composer \
  && rm composer-setup.php
```

### Include WP CLI
```bash
RUN curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar \
    && chmod +x wp-cli.phar \
    && mv wp-cli.phar /usr/local/bin/wp
```

### Node / NPM
```bash
RUN curl -sL https://deb.nodesource.com/setup_15.x | bash - \
  && apt-get install -y nodejs gcc g++ make
```

### Yarn
```bash
RUN curl -sL https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
  && echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list \
  && apt-get update  \
  && apt-get install yarn
```
