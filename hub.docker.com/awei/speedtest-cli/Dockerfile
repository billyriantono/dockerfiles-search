FROM python:3.7-alpine
LABEL MAINTAINER=AwEi \
      GITHUB="https://github.com/chenwei791129/docker-speedtest-cli" \
      DOCKERHUB="https://hub.docker.com/r/awei/speedtest-cli"

ENV CLI_VERSION=2.1.2

RUN pip install --no-cache-dir speedtest-cli==${CLI_VERSION}

ENTRYPOINT ["speedtest-cli"]
