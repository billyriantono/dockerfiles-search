FROM python:3.7-slim-buster

MAINTAINER Borja Toron "borja.toron@gmail.com"

RUN apt-get update -y && \
    apt-get install -y python-pip python-dev

# We copy just the requirements.txt first to leverage Docker cache
COPY ./viewer-002/requirements.txt /app/requirements.txt

WORKDIR /app

RUN pip install -r requirements.txt

RUN mkdir ../common

COPY  ./common/ /common
COPY ./viewer-002 /app

EXPOSE 8000

CMD ["gunicorn" , "--config","/app/conf/gunicorn_config.py" , "app:app"]
