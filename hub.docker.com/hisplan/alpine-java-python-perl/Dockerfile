FROM hisplan/alpine-java-python
MAINTAINER Jaeyoung Chun (chunj@mskcc.org)

LABEL maintainer="chunj@mskcc.org" \
      version="1.0"

RUN apk add --update perl \
    && pip install --upgrade pip \
    && rm -rf /var/cache/apk/*
      
CMD ["/bin/bash"]

