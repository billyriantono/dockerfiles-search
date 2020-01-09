FROM python:3.6
MAINTAINER Vladimir Prudnikov, v.prudnikov@gmail.com
# Python
RUN apt-get update && \
    apt-get upgrade -y


# AWS CLI needs the PYTHONIOENCODING environment varialbe to handle UTF-8 correctly:
ENV PYTHONIOENCODING=UTF-8

RUN apt-get install -y \
    less \
    nodejs \
    npm \
    man \
    rsync \
    python-virtualenv


RUN pip install awscli boto3 

ONBUILD RUN virtualenv /env/zcz-prod
ONBUILD ADD requirements_zcz.txt /app/zcz-prod
ONBUILD RUN /env/zcz-prod/bin/pip install -r /app/zcz-prod/requirements_zcz.txt

RUN npm install -g webpack
# RUN npm install
