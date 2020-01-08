FROM python:3.7.4-alpine
LABEL maintainer="nobia <nobia@icloud.com>"

ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

#ENV SECRET_KEY abc
#ENV DB_HOST 47.88.216.49
#ENV DB_NAME djangot1
#ENV DB_USER djangot1
#ENV DB_PASS djangot1
#ENV SSDB_HOST 47.88.216.49
#ENV SSDB_NAME heavenms
#ENV SSDB_USER djangot1
#ENV SSDB_PASS djangot1
#ENV DEBUG 1

ENV BASE_DIR /base_dir
WORKDIR $BASE_DIR

COPY ./requirements.txt requirements.txt

RUN pip install --upgrade pip

RUN apk update \
    && apk add python3-dev gcc postgresql-dev git \
    && apk add mariadb-dev mariadb-client build-base

RUN pip install -r requirements.txt

ADD https://api.bitbucket.org/2.0/repositories/altasssan/ss-django/commits /dev/null

RUN git clone https://altasssan@bitbucket.org/altasssan/ss-django.git

WORKDIR $BASE_DIR/ss-django


# CMD python manage.py runserver 0.0.0.0:8000