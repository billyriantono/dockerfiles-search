FROM debian:stretch-slim

RUN apt-get update -y && apt-get install -y python-pip && apt-get clean all

RUN pip install ansible==2.4.2.0
