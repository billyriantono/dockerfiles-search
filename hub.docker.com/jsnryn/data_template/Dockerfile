FROM python:slim-stretch

WORKDIR /app

COPY requirements.txt /app/requirements.txt
RUN pip install -r requirements.txt

RUN apt-get update
RUN apt-get --assume-yes install g++
RUN apt-get --assume-yes install unixodbc-dev
RUN pip install pyodbc
