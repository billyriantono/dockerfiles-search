FROM python:3.6.6-alpine3.8

RUN apk --update add gcc make g++ linux-headers && \
    rm -rf /var/cache/apk/* && \
    mkdir /project

ADD . /project

RUN pip install -r /project/requirements.txt

WORKDIR /project
EXPOSE 8000/tcp
ENTRYPOINT ["uwsgi", "/project/demo/uwsgi.ini"]
