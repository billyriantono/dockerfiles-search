FROM python:3.7.0

RUN apt-get update -y
RUN apt-get upgrade -y
RUN pip install --upgrade pip

RUN mkdir -p /app
WORKDIR /app
ADD . /app
RUN pip install -r requirements.txt

VOLUME /app

EXPOSE 8000
