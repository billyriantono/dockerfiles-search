FROM phusion/baseimage
MAINTAINER neil "qazwsxedccsqzse@gmail.com"
RUN apt-get update
RUN apt-get install -y curl && apt-get install -y sudo
RUN curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
RUN apt-get install -y build-essential
RUN apt-get install -y nodejs