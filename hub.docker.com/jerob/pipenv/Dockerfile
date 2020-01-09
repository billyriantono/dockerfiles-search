FROM python:3-slim as build

WORKDIR /app
RUN pip install --upgrade pip
RUN pip install pipenv

ENTRYPOINT ["pipenv"]
