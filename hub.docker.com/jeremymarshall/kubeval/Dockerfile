FROM garethr/kubeval:latest

COPY . /schema/

env KUBEVAL_SCHEMA_LOCATION=file:///schema

RUN mkdir /work
WORKDIR /work

