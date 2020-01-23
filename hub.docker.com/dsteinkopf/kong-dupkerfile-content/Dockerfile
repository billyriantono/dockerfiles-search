# base image
FROM python:3.8.1-alpine

#
RUN apk add gcc musl-dev

ADD ./requirements.txt .

# install requirements
RUN pip install -U pip
RUN pip install -r requirements.txt

