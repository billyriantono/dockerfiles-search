FROM marcospereira/docker-python3-gunicorn-psycopg2:latest

LABEL maintainer="marcospereira.mpj@gmail.com"

RUN apk update && \
    apk upgrade

ADD django_app/ /app/
RUN pip3 install -r /app/requirements.txt

EXPOSE 80

WORKDIR /app

CMD gunicorn -b :80 config.wsgi

