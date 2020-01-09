FROM python:3

MAINTAINER vasily@dubinin.org

# For Python (Pipenv)
ENV LC_ALL C.UTF-8
ENV LANG C.UTF-8

RUN apt-get update && apt-get upgrade -y
#RUN apt-get install nginx -y
#RUN apt-get install python3 python3-pip nginx -y

RUN adduser --disabled-password --gecos "" diary

WORKDIR /home/diary

COPY Pipfile Pipfile
COPY Pipfile.lock Pipfile.lock
RUN pip3 install --upgrade pip
RUN pip3 install pipenv
RUN set -ex && pipenv install --dev --deploy --system --ignore-pipfile

USER diary
COPY app app
COPY migrations migrations
COPY diary.py config.py boot.sh uwsgi.ini ./
#COPY data-dev.sqlite ./data.sqlite

# root needed for nginx
#USER root

# run-time configuration
EXPOSE 5000
ENTRYPOINT ["./boot.sh"]