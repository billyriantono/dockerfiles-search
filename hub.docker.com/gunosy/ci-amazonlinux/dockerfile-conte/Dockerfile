FROM python:3.5

MAINTAINER guillermo "guillermo.trespalacios@gmail.com"

RUN apt-get update && \
      apt-get install -y wget 

COPY requirements.txt /opt

RUN pip install -r /opt/requirements.txt

