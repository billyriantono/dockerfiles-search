FROM ubuntu:latest
MAINTAINER Stepan Yudin <stepan.sib@gmail.com>

ENV REFRESHED_AT 2018–08-23

RUN apt-get update && apt-get install -y \
  build-essential \
  curl \
  zip \
  unzip \
  wget \
  git \
  mc \
  iputils-ping \
  faketime \
  cron \
  mc \
  sudo \
  iputils-ping
  
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash -
RUN apt-get update && apt-get install -y nodejs

RUN npm install -g @vue/cli

# Create workdir
RUN mkdir -p /var/www/frontend

# Create www-data sudoer user
RUN adduser www-data sudo
RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers
RUN usermod -u 1000 www-data
RUN chown -R www-data:www-data /var/www

EXPOSE 8080
USER www-data
WORKDIR /var/www/frontend
