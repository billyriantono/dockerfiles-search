FROM ubuntu:trusty
MAINTAINER Aurelio Santos <aurex@dizenia.me>

ENV DEBIAN_FRONTEND noninteractive
RUN locale-gen es_MX.UTF-8; \
    locale-gen en_US.UTF-8
ENV LANG       es_MX.UTF-8
ENV LC_ALL     es_MX.UTF-8

RUN echo America/Mazatlan | tee /etc/timezone && dpkg-reconfigure --frontend noninteractive tzdata
