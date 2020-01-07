FROM ubuntu:latest
MAINTAINER Rajdeep Dua "joyesong@qq.com"
RUN apt-get update -y
RUN apt-get install -y python-pip python-dev build-essential
RUN apt-get autoremove
COPY . /app
WORKDIR /app
RUN pip install -r requirements.txt
