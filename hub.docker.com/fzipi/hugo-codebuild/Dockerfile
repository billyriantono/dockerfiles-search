# Dockerfile for checking local changes made to the oss8 site using hugo.

# Run the following commands to setup this docker
# docker pull ubuntu:16.04
# git clone https://github.com/OpenSecuritySummit/oss2019.git 
# cd oss2019 && git clone https://github.com/devcows/hugo-universal-theme.git themes/oss-owasp
# docker build -t oss2019 . 
# docker run -it -p 1313:1313 -v $(pwd):/opt/oss2019 oss2019:latest 

FROM ubuntu:16.04
LABEL authors="Mohammed A. Imran <imran.mohammed@owasp.org>, Felipe Zipitria <felipe.zipitria@owasp.org>"

ENV DEBIAN_FRONTEND=noninteractive
ENV HUGO_VERSION="0.55.5"
ENV SRC_DIR="/opt/oss2019"

RUN apt-get update \
    && apt-get install -y curl git awscli tar \
    && adduser --disabled-password --gecos "oss" oss  \
    && curl -Ls https://github.com/gohugoio/hugo/releases/download/v${HUGO_VERSION}/hugo_extended_${HUGO_VERSION}_Linux-64bit.tar.gz -o /tmp/hugo.tar.gz \
    && tar xf /tmp/hugo.tar.gz -C /usr/local/bin \
    && rm -rf /var/lib/apt/lists/* /tmp/hugo.tar.gz \
    && mkdir -p $SRC_DIR

WORKDIR $SRC_DIR
ADD --chown=oss:oss . $SRC_DIR

USER oss:oss

