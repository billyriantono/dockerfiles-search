FROM ubuntu:14.04

RUN sed -i '1ideb mirror://mirrors.ubuntu.com/mirrors.txt precise-updates main restricted universe multiverse' /etc/apt/sources.list
RUN sed -i '1ideb mirror://mirrors.ubuntu.com/mirrors.txt precise-backports main restricted universe multiverse' /etc/apt/sources.list
RUN sed -i '1ideb mirror://mirrors.ubuntu.com/mirrors.txt precise-security main restricted universe multiverse' /etc/apt/sources.list
RUN apt-get update

RUN apt-get install -y mono-complete libmysqlclient15-dev