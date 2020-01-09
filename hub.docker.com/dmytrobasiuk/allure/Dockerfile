FROM openjdk:8-jre

COPY allure-2.7.0.tgz /

RUN apt-get update \
    && apt-get install tar \
    && tar -xvf allure-2.7.0.tgz \
    && chmod -R +x /allure-2.7.0/bin

VOLUME ["/allure-report"]
VOLUME ["/report/allure-results"]

WORKDIR /allure-2.7.0/bin
