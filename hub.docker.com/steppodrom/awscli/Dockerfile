FROM python:3.7-alpine

RUN apk --no-cache --update add && \
pip install --no-cache-dir awscli

ENTRYPOINT ["aws"]
