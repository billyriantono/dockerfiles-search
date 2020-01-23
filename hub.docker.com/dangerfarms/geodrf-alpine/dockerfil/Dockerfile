FROM alpine

ENV SOURCE=https://github.com/UKHomeOffice/repo-security-scanner/releases/download/0.3.1/
ENV FILE_NAME=scanrepo-0.3.1-linux-amd64.tar.gz

RUN apk add --update git wget tar && \
    rm -rf /var/cache/apk/*

RUN \
  wget ${SOURCE}${FILE_NAME} && \
  tar -zxvf ${FILE_NAME} && \
  chmod +X ./scanrepo && \
  mv scanrepo /usr/bin/scanrepo

ENTRYPOINT ["git log -p | scanrepo "]
