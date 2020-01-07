FROM alpine:3.7
MAINTAINER reizist <reizist@gmail.com>

ENV HUGO_VERSION 0.50
ENV HUGO_BINARY hugo_${HUGO_VERSION}_linux-64bit

RUN apk update && apk add git && apk add openssh && rm -rf /var/cache/apk/*

# Download and Install hugo
RUN mkdir /usr/local/hugo
ADD https://github.com/spf13/hugo/releases/download/v${HUGO_VERSION}/${HUGO_BINARY}.tar.gz /usr/local/hugo/
RUN tar xzf /usr/local/hugo/${HUGO_BINARY}.tar.gz -C /usr/local/hugo/ \
	&& ln -s /usr/local/hugo/hugo /usr/local/bin/hugo \
	&& rm /usr/local/hugo/${HUGO_BINARY}.tar.gz

EXPOSE 1313
CMD hugo version
