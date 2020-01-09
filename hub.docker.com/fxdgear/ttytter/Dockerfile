FROM alpine
MAINTAINER Nick Lang <nick.lang@docker.com>

RUN apk --update add curl perl
RUN curl -L http://www.floodgap.com/software/ttytter/dist2/2.1.00.txt > /usr/bin/ttyttr
RUN chmod +x /usr/bin/ttyttr
RUN apk del curl  && rm -rf /var/cache/apk/*
VOLUME ["/data"]

ENTRYPOINT ["/usr/bin/ttyttr", "-keyf=/data/.ttytterkey"]
