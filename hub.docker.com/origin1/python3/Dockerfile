FROM ubuntu:18.04

ENV LANG C.UTF-8
RUN apt-get update && apt-get install -y python3.5 python-pip virtualenv
RUN pip install setuptools pip --upgrade
RUN pip install pytz --upgrade
RUN virtualenv /venv/testenv/ -p python3
