FROM debian:stretch-slim

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get install -y zip python-pip python-dev build-essential
RUN pip install --upgrade pip
RUN pip install --upgrade virtualenv
RUN pip install boto3==1.4.7

ADD s3_upload /usr/local/bin
RUN chmod u+x /usr/local/bin/s3_upload
