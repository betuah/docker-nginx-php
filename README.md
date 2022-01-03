# Docker PHP-FPM 7 & Nginx on Alpine Linux
Example PHP-FPM 7 & Nginx container image for Docker, build on [Alpine Linux](https://www.alpinelinux.org/).

Repository: https://github.com/betuah/docker-nginx-php

* Built on the lightweight and secure Alpine Linux distribution
* Multi-platform, supporting AMD4, ARMv6, ARMv7, ARM64
* Uses PHP 7 for better performance, lower CPU usage & memory footprint
* Optimized for 1000 concurrent users
* Optimized to only use resources when there's traffic (by using PHP-FPM's `on-demand` process manager)
* The services Nginx, PHP-FPM and supervisord run under a non-privileged user (nobody) to make it more secure
* The logs of all the services are redirected to the output of the Docker container (visible with `docker logs -f <container name>`)
* Follows the KISS principle (Keep It Simple, Stupid) to make it easy to understand and adjust the image to your needs

![nginx 1.20](https://img.shields.io/badge/nginx-1.20-brightgreen.svg)
![php 7.0](https://img.shields.io/badge/php-8.0-brightgreen.svg)
![License MIT](https://img.shields.io/badge/license-MIT-blue.svg)

## Goal of this project
The goal of this container image is to provide an example for running Nginx and PHP-FPM in a container which follows
the best practices and is easy to understand and modify to your needs.

## Usage

Start the Docker container:

    docker run -p 80:8080 betuah/php-nginx

See the PHP info on http://localhost/info.php, or the static html page with upload file on http://localhost

Or mount your own code to be served by PHP-FPM & Nginx

    docker run -p 80:8080 -v ~/my-codebase:/var/www/html betuah/php-nginx

## Configuration
In [config/](config/) you'll find the default configuration files for Nginx, PHP and PHP-FPM.
If you want to extend or customize that you can do so by mounting a configuration file in the correct folder;

Nginx configuration:

    docker run -v "`pwd`/config/nginx/nginx.conf:/etc/nginx/nginx.conf" betuah/php-nginx

PHP configuration:

    docker run -v "`pwd`/config/php/php.ini:/etc/php7/conf.d/custom.ini" betuah/php-nginx

PHP-FPM configuration:

    docker run -v "`pwd`/config/php/php-fpm.conf:/etc/php7/php-fpm.d/www.conf" betuah/php-nginx

_Note; Because `-v` requires an absolute path I've added `pwd` in the example to return the absolute path to the current directory_
