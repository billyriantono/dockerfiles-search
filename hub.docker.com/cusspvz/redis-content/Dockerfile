FROM python:3.4-slim

RUN apt-get update && apt-get -y install groff less && apt-get clean
RUN pip install awscli

ENTRYPOINT ["/usr/local/bin/aws"]
