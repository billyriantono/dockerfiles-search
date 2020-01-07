FROM golang:1.11-alpine

RUN apk add --no-cache \
        docker \
        make \
		py-pip

RUN pip install --upgrade pip && \
    pip install docker-compose

