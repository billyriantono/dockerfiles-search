FROM anapsix/alpine-java
MAINTAINER Xinfeng Zhang

RUN mkdir /allure
RUN mkdir /allure-results
RUN mkdir /allure-report
RUN mkdir /allure-config

RUN apk update

RUN wget https://dl.bintray.com/qameta/generic/io/qameta/allure/allure/2.7.0/allure-2.7.0.tgz
RUN tar -xvf allure-2.7.0.tgz -C /allure
ENV PATH="/allure/allure-2.7.0/bin:${PATH}"
ENV ALLURE_CONFIG="/allure-config/allure.properties"
