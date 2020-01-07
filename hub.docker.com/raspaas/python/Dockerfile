FROM python:2.7.10

ENV PORT 5000
EXPOSE 5000

RUN mkdir /app
WORKDIR /app

ONBUILD ADD ./requirements.txt requirements.txt
ONBUILD RUN pip install --no-cache-dir -r requirements.txt

ONBUILD ADD . /app
