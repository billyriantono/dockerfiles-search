FROM python:3.7-alpine
LABEL author="Prometej"

RUN apk update \
    && apk upgrade \
    && apk add git \
    && pip install pipenv

WORKDIR /test

COPY lab5/test/requirements.txt ./
RUN pipenv install -r requirements.txt

COPY lab5/test/ ./

ENTRYPOINT pipenv run pytest test_app.py --url http://app:5000
