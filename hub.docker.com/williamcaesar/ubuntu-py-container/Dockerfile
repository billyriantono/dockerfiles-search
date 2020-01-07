FROM ubuntu:18.04
MAINTAINER WilliamCaesar

ENV PYTHONUNBUFFERED 1
ENV LANG C.UTF-8

ENV TZ=UTC
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN apt-get update
RUN apt-get install cron python3.7 -y
RUN apt install python3-pip -y
RUN apt-get autoclean
CMD ["python"]
