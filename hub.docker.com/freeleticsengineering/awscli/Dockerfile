FROM python:2-alpine
MAINTAINER Freeletics GmbH <operations@freeletics.com>

RUN pip install --upgrade pip
RUN pip install awscli

WORKDIR /aws
ENTRYPOINT ["aws"]
