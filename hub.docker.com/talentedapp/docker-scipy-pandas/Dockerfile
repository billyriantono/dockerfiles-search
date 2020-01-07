FROM python:3.6-alpine3.8
ENV PYTHONUNBUFFERED 1

RUN echo "@community http://dl-cdn.alpinelinux.org/alpine/edge/community" >> /etc/apk/repositories
RUN apk add --update --no-cache openblas-dev@community gfortran

RUN apk add --no-cache \
  build-base

RUN mkdir /app
WORKDIR /app

RUN pip install --no-cache-dir scipy==1.1.0 pandas==0.23.3 numpy==1.15.0
RUN pip install --no-cache-dir scikit-learn==0.19.2