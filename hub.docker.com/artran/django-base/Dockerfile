FROM python:2.7

MAINTAINER Ray Tran <ray@artran.co.uk>

ENV PYTHONUNBUFFERED 1

COPY requirements.txt /tmp/
RUN pip install -q --upgrade pip && pip install -r /tmp/requirements.txt

EXPOSE 8000
