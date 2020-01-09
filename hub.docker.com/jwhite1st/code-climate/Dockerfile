FROM python:alpine

RUN apk add --no-cache curl gcc
RUN curl -L https://codeclimate.com/downloads/test-reporter/test-reporter-latest-linux-amd64 > ./cc-test-reporter && chmod +x cc-test-reporter
RUN ./cc-test-reporter before-build
RUN pip3 install coverage && coverage --version