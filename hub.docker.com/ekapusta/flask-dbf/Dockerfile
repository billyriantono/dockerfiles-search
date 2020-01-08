FROM python:3
MAINTAINER Dmitry Romanov "dmitry.romanov85@gmail.com"

RUN ["pip", "install", "Flask"]
RUN ["pip", "install", "flask-autodoc"]
RUN ["pip", "install", "dbf"]
RUN ["pip", "install", "PyYAML"]
RUN ["pip", "install", "gunicorn"]
RUN ["pip", "install", "mysqlclient"]

VOLUME ["/code"]
WORKDIR /code
