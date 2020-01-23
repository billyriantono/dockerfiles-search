FROM weahead/chmod

MAINTAINER We ahead <docker@weahead.se>

ENV CONFD_VERSION 0.11.0

ADD https://github.com/kelseyhightower/confd/releases/download/v${CONFD_VERSION}/confd-${CONFD_VERSION}-linux-amd64 /confd

RUN ["/chmod", "+x", "/confd"]
