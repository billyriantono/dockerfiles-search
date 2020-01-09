FROM python:3.6-alpine

RUN apk --update add build-base freetype-dev gfortran libpng-dev openblas-dev

COPY requirements.txt /

RUN pip install -v -r /requirements.txt
