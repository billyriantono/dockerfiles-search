FROM mcr.microsoft.com/dotnet/core/sdk:2.2-alpine

RUN apk add --no-cache --virtual .build-deps g++ python3-dev libffi-dev openssl-dev && \
  apk add --no-cache --update bash python3 && \
  pip3 install --upgrade pip setuptools && \
  pip3 install boto3 jsonschema wait

WORKDIR /app