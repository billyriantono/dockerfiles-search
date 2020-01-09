# base image
FROM rocker/r-base

MAINTAINER Norbert Walchhofer <nw@cognify.ai>
RUN apt-get update -qq && apt-get -y upgrade \
 && apt-get -y install libxml2-dev libpq-dev libmariadbclient-dev libcurl4-openssl-dev libssl-dev libcairo2-dev libudunits2-dev libgdal-dev libgeos-dev libssh2-1-dev libgit2-dev openjdk-8-jdk-headless libaio1 python3-pip python3-dev libpython3-dev \
 && rm -rf /tmp/* && apt-get autoremove -y && apt-get autoclean -y && rm -rf /var/lib/apt/lists/* \
 && ln -s /usr/lib/jvm/java-8-openjdk-amd64/ /usr/lib/jvm/default-java \
 && R CMD javareconf

ENV JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64

CMD ["/usr/bin/R"]