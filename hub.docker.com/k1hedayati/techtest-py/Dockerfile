FROM python:3.6-alpine

LABEL appname="aylien-techtest-py"
LABEL maintainer="Zoltan Csiffary (zoltan.csiffary@gmail.com)"
LABEL version="0.0.1"
LABEL description="Aylien technical challenge"

EXPOSE 8080 8081
WORKDIR /app

COPY app/Makefile /app
COPY app/requirements.txt /app

RUN set -eux; \
	  apk add --no-cache ca-certificates curl && \
    apk add --no-cache --virtual make && \
    make && \
	  make build && \
	  apk del make && \
	  rm -rf /var/cache/apk/*

COPY app /app

CMD ["python", "app.py", "--port", "8080", "--monitor", "8081"]
