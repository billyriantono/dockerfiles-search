FROM alpine:3.7
LABEL version="1.1.0"
LABEL maintainer="Michal Ochman <michal@kalambagames.com>"

RUN \
  apk -v --update add \
    git \
    git-lfs \
    jq \
    openssh-client \
    python3 \
    rsync \
    zip && \
  pip3 install --upgrade pip && \
  pip3 install --upgrade awscli && \
  aws configure set preview.cloudfront true && \
  rm /var/cache/apk/*