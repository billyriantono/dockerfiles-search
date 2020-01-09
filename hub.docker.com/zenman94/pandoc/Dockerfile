FROM alpine:3.8
MAINTAINER Gaëtan Ars <zenman94@free.fr>

ENV PANDOC_VERSION 2.4

RUN wget -qO- https://github.com/jgm/pandoc/releases/download/${PANDOC_VERSION}/pandoc-${PANDOC_VERSION}-linux.tar.gz | tar xzf - && \
    mv pandoc-${PANDOC_VERSION}/* /usr/local && \
    chmod +x /usr/local/bin/pandoc*

CMD ["sh"]
