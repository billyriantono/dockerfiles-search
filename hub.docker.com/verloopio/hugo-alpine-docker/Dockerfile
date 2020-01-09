FROM alpine:3.7
MAINTAINER Avinash Sajjanshetty <hi@avi.im>

ENV HUGO_VERSION 0.36

ADD https://github.com/gohugoio/hugo/releases/download/v${HUGO_VERSION}/hugo_${HUGO_VERSION}_Linux-64bit.tar.gz /hugo-source/
RUN tar -xf /hugo-source/hugo_${HUGO_VERSION}_Linux-64bit.tar.gz -C /hugo-source && mv /hugo-source/hugo /usr/local/bin/hugo && rm -rf /hugo-source

EXPOSE 1313