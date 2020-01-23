FROM python:3.6-slim

COPY ./app /app
WORKDIR /
RUN apt-get update &&\
    apt-get install -y libpq-dev python3-dev gcc
RUN pip install -r /app/requirements.txt
CMD celery worker -A app.runcelery:celery --loglevel=info --uid=nobody