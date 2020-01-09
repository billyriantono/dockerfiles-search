FROM python:alpine3.7

WORKDIR /code

RUN apk update && apk add --no-cache docker

COPY imager.py /code/

CMD python imager.py

