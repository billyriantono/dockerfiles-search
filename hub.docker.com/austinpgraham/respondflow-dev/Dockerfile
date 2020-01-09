FROM ubuntu:latest
MAINTAINER Austin Graham "austin.graham@simonsaysapps.com"

RUN apt-get update -y --fix-missing
RUN apt-get install -y python3-pip python3-dev build-essential libffi-dev libpq-dev
RUN rm -rf /usr/lib/python3/dist-packages/setuptools*
RUN pip3 install --upgrade pip
RUN pip3 install setuptools
RUN pip3 install requests
RUN pip3 install gevent

COPY . /

WORKDIR /

RUN python3 setup.py develop
EXPOSE 80
CMD gunicorn --paste conf/rfdev.external.ini --timeout 100
