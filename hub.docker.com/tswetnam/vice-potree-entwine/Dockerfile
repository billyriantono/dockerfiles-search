FROM python:3.7-alpine

RUN apk add git

RUN git clone https://github.com/connormanning/potree.entwine.io /potree.entwine.io

WORKDIR /potree.entwine.io

EXPOSE 8000
EXPOSE 443

ENTRYPOINT python3 -s -m http.server 8000 --directory /potree.entwine.io
