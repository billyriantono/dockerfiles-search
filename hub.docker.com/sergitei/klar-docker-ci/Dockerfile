FROM quay.io/coreos/clair:latest

RUN apk --no-cache upgrade
RUN apk add --no-cache curl py-pip \
 && curl -L https://github.com/optiopay/klar/releases/download/v2.1.0/klar-2.1.0-linux-amd64 \
  > /usr/local/bin/klar \
 && chmod +x /usr/local/bin/klar \
 && pip install awscli

ADD config.yaml /etc/clair/config.yaml
ADD entrypoint.sh /
ADD klar-docker-ci.sh /usr/local/bin/klar-docker-ci

ENV CLAIR_ADDR http://localhost:6060

ENTRYPOINT [ "/entrypoint.sh" ]
