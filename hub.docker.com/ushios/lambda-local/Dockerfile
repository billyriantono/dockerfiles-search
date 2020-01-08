FROM python:2.7-alpine
LABEL maintainer "UshioShugo<ushio.s@gmail.com>"

ENV SOURCE_DIR "/opt/lambda"

RUN [ "pip", "install", "python-lambda-local==0.1.3" ]

ADD . $SOURCE_DIR
WORKDIR $SOURCE_DIR
