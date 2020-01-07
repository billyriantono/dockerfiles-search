FROM python:3.7

# install wget
RUN apt-get -y update
RUN apt-get install -y mysql-client curl
RUN pip install virtualenv

# set display port to avoid crash
ENV DISPLAY=:99