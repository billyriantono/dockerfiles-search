FROM ubuntu:14.04

RUN apt-get update && apt-get install -y \
	git \
	python-dev \
	python-pip \
	liblapack-dev \
	gfortran

WORKDIR /root
COPY requirements.txt /root/requirements.txt

RUN pip install -r requirements.txt

EXPOSE 3001