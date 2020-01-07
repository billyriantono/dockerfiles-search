FROM python:3.6-alpine
RUN apk update \
  && apk add --virtual build-deps gcc python3-dev musl-dev libffi-dev \
  && apk add postgresql-dev \
  && apk add libxml2-dev libxslt-dev \
  && pip install psycopg2 \
  && pip install lxml==4.2.5 \
  && pip install scrapy \
  && apk del build-deps
