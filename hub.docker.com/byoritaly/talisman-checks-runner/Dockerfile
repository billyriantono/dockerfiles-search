FROM ubuntu:latest

RUN apt-get update && \
    apt-get install -y curl git

ARG TALISMAN_VERSION="0.4.6"
RUN curl -L "https://github.com/thoughtworks/talisman/releases/download/v${TALISMAN_VERSION}/talisman_linux_amd64" > /usr/bin/talisman && \
    chmod +x /usr/bin/talisman

WORKDIR /usr/src

CMD [ "/bin/bash", "-c", "talisman --version" ]
