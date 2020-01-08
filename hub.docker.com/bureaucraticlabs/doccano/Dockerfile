FROM python:3.6-slim
RUN mkdir -p /usr/src
WORKDIR /usr/src
ADD . /usr/src/doccano 
WORKDIR /usr/src/doccano
RUN pip install -r requirements.txt
WORKDIR /usr/src/doccano/app
