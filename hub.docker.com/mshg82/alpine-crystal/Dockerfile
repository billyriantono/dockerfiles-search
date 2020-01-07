FROM alpine:3.8
RUN apk update && apk add wget build-base libressl-dev zlib-dev
RUN wget https://github.com/crystal-lang/crystal/releases/download/0.27.0/crystal-0.27.0-1-linux-x86_64.tar.gz
RUN tar -zxvf crystal-0.27.0-1-linux-x86_64.tar.gz
RUN mv /crystal-0.27.0-1/bin/* /usr/local/bin/
RUN mv /crystal-0.27.0-1/lib/* /usr/local/lib/
RUN rm -r crystal-0.27.0-1*
RUN rm -rf /var/cache/apk/*

ENTRYPOINT ["sh"]
