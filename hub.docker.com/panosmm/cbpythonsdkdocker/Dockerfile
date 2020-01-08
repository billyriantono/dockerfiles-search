# Use an official Python runtime as a parent image
FROM python:2.7-slim

# couchbase python sdk
RUN apt-get update
RUN apt-get install libevent-dev -y --no-install-recommends
RUN apt-get -y install libev4
RUN apt-get install wget -y

RUN dpkg --configure -a

RUN wget http://packages.couchbase.com/clients/c/libcouchbase-2.8.5_wheezy_amd64.tar
RUN tar xf libcouchbase-2.8.5_wheezy_amd64.tar
RUN dpkg -i libcouchbase-2.8.5_wheezy_amd64/*.deb

RUN apt-get install g++ -y --no-install-recommends
RUN pip install couchbase
