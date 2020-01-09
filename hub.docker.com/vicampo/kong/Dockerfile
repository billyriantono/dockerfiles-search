FROM python:3.6.3-alpine3.6

RUN pip install boto3 requests

COPY . /src
VOLUME ["/src", "/root/.aws"]
WORKDIR /src
