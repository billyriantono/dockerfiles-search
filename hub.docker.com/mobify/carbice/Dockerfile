FROM python:3.5.1-alpine
MAINTAINER Mobify <ops@mobify.com>

ADD . /app
WORKDIR /app

RUN pip install -e .

ENTRYPOINT ["carbice"]
