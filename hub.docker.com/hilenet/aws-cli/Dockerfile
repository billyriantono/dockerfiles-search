FROM python:3.6-alpine
RUN apk add --no-cache --virtual .dep gcc musl-dev \
  && pip3 --no-cache-dir install awscli aws-sam-cli \
  && apk del --purge .dep
EXPOSE 3000
