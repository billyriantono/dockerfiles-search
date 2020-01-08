FROM debian:stretch

MAINTAINER "Jeremy CURNY" <jeremy.curny.pro@gmail.com>

ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update \
    && apt-get install -y apt-transport-https curl cron gnupg htop iftop iotop nano sudo telnet tree wget xmlstarlet zip \
    && apt-get clean autoclean \
    && apt-get autoremove
