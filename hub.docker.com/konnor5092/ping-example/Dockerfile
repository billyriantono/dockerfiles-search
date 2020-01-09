FROM ubuntu

MAINTAINER Matthew O'Connor <matty_o_connor01@hotmail.com>

RUN apt-get update && apt-get install iputils-ping -y

RUN mkdir Selenium

ADD http://selenium-release.storage.googleapis.com/3.9/selenium-server-standalone-3.9.1.jar /Selenium/
ADD Mattstxtfile /Selenium/

WORKDIR /Selenium

ENV JAVA_HOME "Hello World"

EXPOSE 8888
