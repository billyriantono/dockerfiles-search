FROM alpine:3.6
MAINTAINER David Sarrio <sarrio.david@gmail.com> 

RUN apk --no-cache add \
      py-pip \
      python \
    && pip install --upgrade \
      pip \
      boto3==1.4.4 \
    && mkdir ~/.aws

VOLUME ["~/.aws"]

CMD ["/bin/sh"]
