FROM python:3.7.2

ENV PYTHONUNBUFFERED 1
ENV PROJECT_ROOT /usr/src/app

RUN mkdir -p $PROJECT_ROOT

WORKDIR $PROJECT_ROOT
COPY requirements.txt $PROJECT_ROOT

RUN apt-get update -y && pip install --upgrade pip
RUN pip install -r requirements.txt

COPY . $PROJECT_ROOT
