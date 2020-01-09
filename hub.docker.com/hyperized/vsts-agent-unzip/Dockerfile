FROM microsoft/vsts-agent:ubuntu-16.04

LABEL maintainer="Gerben Geijteman <gerben@hyperized.net>"
LABEL description="Microsoft VSTS Agent image with unzip"

RUN apt-get update && \
    apt-get -y install unzip && \
    apt-get -y autoremove && \
    apt-get autoclean

