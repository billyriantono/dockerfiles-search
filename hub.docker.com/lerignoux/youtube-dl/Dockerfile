FROM python:3.7-alpine
MAINTAINER Erignoux Laurent <lerignoux@gmail.com>

RUN pip install youtube-dl
RUN mkdir /Downloads

WORKDIR /Downloads

ENTRYPOINT ["youtube-dl"]
