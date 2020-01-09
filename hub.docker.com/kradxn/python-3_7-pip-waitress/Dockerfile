FROM ubuntu:18.04

ENV LANG C.UTF-8
RUN apt-get update && apt-get install -y python python-dev python3.7 python3.7-dev python-pip virtualenv libssl-dev libpq-dev git build-essential libfontconfig1 libfontconfig1-dev
RUN pip install setuptools pip --upgrade --force-reinstall
RUN virtualenv /venv/testenv/ -p $(which python3.7)
RUN pip install waitress
