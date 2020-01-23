FROM alpine

MAINTAINER Christian Torff <devops@io4c.net>

RUN apk add --update python wget && rm -rf /var/cache/apk/*

RUN wget --no-check-certificate https://github.com/fboender/scriptform/archive/1.0.tar.gz && \
    tar xvzf 1.0.tar.gz && \
    rm -f 1.0.tar.gz && \
    mv scriptform-1.0 scriptform && \
    ln -s /scriptform/src/scriptform.py  /usr/bin/scriptform

EXPOSE 80

ENTRYPOINT ["/usr/bin/scriptform", "-f", "-p80"]

CMD ["--help"]

