FROM python:3.6.7

LABEL maintainer="tomoya@mitsuse.jp"

RUN pip install pipenv

VOLUME /app

ENTRYPOINT cd /app && pipenv install --deploy && pipenv run app
