FROM python:2.7.16-alpine3.10
COPY . /usr/local/src/euvat-json-api

WORKDIR /usr/local/src/euvat-json-api
RUN pip install -U .

ENTRYPOINT ["/usr/local/bin/euvat-json-api"]
