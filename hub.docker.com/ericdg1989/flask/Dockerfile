FROM python:3.7-alpine

RUN apk update && apk add --no-cache tini build-base \
    && pip install flask

EXPOSE 5000
ENTRYPOINT ["/sbin/tini", "--"]