FROM node:10
LABEL maintainer="Craig Sketchley <craig@gradeproof.com>"

RUN apt-get update && apt-get install -y python python-dev
RUN curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
RUN python get-pip.py
RUN pip install --upgrade pip
RUN pip install awscli aws-sam-cli --upgrade
