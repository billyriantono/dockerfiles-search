FROM nginx

MAINTAINER Tobia Dalsecco <tobia.dalsecco@gmail.com>

RUN mkdir /data

WORKDIR /data

RUN apt-get update -y 
RUN apt-get install -y libtool autoconf automake make g++ uuid-dev wget build-essential curl

RUN curl --silent --location https://deb.nodesource.com/setup_0.12 | bash -
RUN apt-get install --yes nodejs

RUN npm install -g bower