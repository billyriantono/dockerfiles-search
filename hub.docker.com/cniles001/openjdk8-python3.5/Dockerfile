FROM openjdk:8

RUN apt-get update

RUN curl -O https://www.python.org/ftp/python/3.5.7/Python-3.5.7.tgz
RUN tar -xzf Python-3.5.7.tgz
RUN apt-get install make build-essential libssl-dev zlib1g-dev libbz2-dev libsqlite3-dev libssl-dev -y
RUN cd Python-3.5.7 && ./configure && make && make install

RUN python3.5 -m ensurepip

