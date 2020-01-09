FROM yuliujuan/pmt:base

MAINTAINER      Amber Yu "liujuan.yu@accenture.com"

ENV FLASK_ENV=production
#ENV UWSGI_INI /application/uwsgi.ini

RUN pip install --upgrade pip

WORKDIR /usr/src
COPY requirements.txt ./
RUN pip install --no-cache-dir -r requirements.txt 

WORKDIR /app
COPY ./pmt /app/pmt
COPY ./uwsgi.ini /app/uwsgi.ini
