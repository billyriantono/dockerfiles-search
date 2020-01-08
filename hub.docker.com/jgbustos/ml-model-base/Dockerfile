# this is an official Python runtime, used as the parent image
FROM python:3.6-slim-buster

LABEL maintainer="j.garciadebustos@godeltech.com"

COPY . /app
WORKDIR /app
 
RUN pip install --upgrade pip \
  && pip install -r requirements.txt

ENTRYPOINT ["python3"]
