############################################################
# Dockerfile
############################################################

# Extends: PHP 7 - Apache (Debian)
FROM php:7-apache

############################################################
# Environment Configuration
############################################################

############################################################
# Installation
############################################################

# Install packages. Notes:
#   * git: a git client to check out repositories
ENV PACKAGES="\
  git \
  curl \
  wget \
  unzip \
  zlib1g-dev \
  libpng-dev \
"

RUN echo "Installing Packages ..." &&\
	# Update Package List
	apt-get update &&\
	# Package Install [no-cache, because the cache would be within the build - bloating up the file size]
	apt-get install $PACKAGES -y &&\
	# PHP Extensions
	docker-php-ext-install pdo_mysql &&\
	docker-php-ext-install mbstring &&\
	docker-php-ext-install zip &&\
	docker-php-ext-install gd &&\
	# WebTrees
	wget -q https://github.com/fisharebest/webtrees/releases/download/1.7.9/webtrees-1.7.9.zip &&\
	unzip webtrees-*.zip -d /var/www/html &&\
	mv /var/www/html/webtrees/* /var/www/html &&\
	chown -R www-data:www-data  /var/www/html &&\
	rm -rf webtrees-*.zip /var/www/html/webtrees &&\
	echo "Installation complete ..."

# Copy files from rootfs to the container
ADD rootfs /

# Build CleanUp
## Removes all packages that have been flagged as build dependencies
RUN echo "CleanUp ..."

############################################################
# Execution
############################################################
