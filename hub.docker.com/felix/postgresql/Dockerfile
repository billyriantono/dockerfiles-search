FROM ubuntu:12.04

RUN echo 'deb http://de.archive.ubuntu.com/ubuntu/ precise main restricted universe' > /etc/apt/sources.list
RUN apt-get update
RUN apt-get -y install wget ca-certificates
# http://www.postgresql.org/download/linux/ubuntu/
RUN echo 'deb http://apt.postgresql.org/pub/repos/apt/ precise-pgdg main' > /etc/apt/sources.list.d/pdgd.list
RUN wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add -
RUN apt-get update
RUN apt-get -y install postgresql-9.3

