FROM alpine:latest
RUN apk add --update curl
ENV PATH $PATH:/root/.local/bin
RUN curl -sSL https://get.haskellstack.org/ | sh
RUN stack new site
WORKDIR site

RUN stack setup --resolver lts-8.13

RUN stack install hakyll
RUN hakyll-init .

RUN stack init
RUN stack build
RUN stack exec site build
#
