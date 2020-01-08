FROM python:3.6.6

RUN apt-get update
RUN apt-get install -y sudo build-essential
RUN apt-get install -y postgis libpq-dev
RUN apt-get install -y python3-dev gettext
RUN pip install -U tox
