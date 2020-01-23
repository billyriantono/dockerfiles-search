FROM alpine:3.7

ENV HUGO_VERSION 0.40.1
ENV HUGO_HANDLE hugo_${HUGO_VERSION}_Linux-64bit
ENV HUGO_ARCHIVE ${HUGO_HANDLE}.tar.gz
ENV HUGO_URL https://github.com/spf13/hugo/releases/download/v${HUGO_VERSION}/${HUGO_ARCHIVE}

WORKDIR /hugo

ADD ${HUGO_URL} ./

RUN tar xzf ${HUGO_ARCHIVE} && \
    mv hugo /usr/local/bin/hugo && \
    rm -r *.*

EXPOSE 1313

ENTRYPOINT ["hugo"]
