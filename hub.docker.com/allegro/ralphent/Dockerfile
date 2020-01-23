FROM ubuntu:14.04
MAINTAINER Chi-Wen Fann <allanfann@gmail.com>
 
# Import scrapy signing key
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 627220E7

# Create an apt sources.list file
RUN echo 'deb http://archive.scrapy.org/ubuntu scrapy main' | tee /etc/apt/sources.list.d/scrapy.list

# update source list
RUN apt-get update -y
 
# Install scrapy
RUN apt-get -y install scrapy-0.24 git

# create working directory
RUN mkdir /app

# change working directory
WORKDIR /app



