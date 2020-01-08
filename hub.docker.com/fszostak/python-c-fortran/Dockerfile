FROM python:3.8-buster 
LABEL maintainer="fszostak@gmail.com"

RUN apt-get update && apt-get -y install build-essential python3-dev gfortran python3-numpy
RUN apt-get clean && rm -rf /var/lib/apt/lists/
RUN pip3 install --upgrade numpy
