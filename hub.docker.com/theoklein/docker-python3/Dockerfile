FROM ubuntu:xenial
MAINTAINER Theo <theokleintw@gmail.com>

RUN apt-get update && apt-get install -y \
    python3 \
    python3-pip

RUN pip3 install --upgrade pip
RUN pip3 install -U \
	gensim \
	pymongo \
	flask \
	telepot \
	line-bot-sdk

RUN rm -rf /var/lib/apt/lists/*
