FROM openjdk:8-jre

COPY allure-2.12.1.tar.gz /

RUN apt-get update \
    && apt-get install tar \
    && tar -xvf allure-2.12.1.tar.gz \
    && chmod -R +x /allure-2.12.1/bin

VOLUME ["/allure-results"]
VOLUME ["/allure-report"]

WORKDIR /allure-2.12.1/bin