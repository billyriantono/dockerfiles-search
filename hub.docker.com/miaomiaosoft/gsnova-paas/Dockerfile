FROM alpine:3.6

ENV VER=latest

RUN \
    apk add --no-cache --virtual  curl \
    && mkdir -m 777 /gsnova \
    && cd /gsnova \
    && curl -fSL https://github.com/yinqiwen/gsnova/releases/download/$VER/gsnova_linux_amd64-$VER.tar.bz2 | tar xj  \
    && rm -rf server.json \
    && rm -rf gsnova_linux_amd64-$VER.tar.bz2 \
    && chgrp -R 0 /gsnova \
    && chmod -R g+rwX /gsnova 
    
ADD server.json /gsnova/server.json    

CMD ["/gsnova/gsnova","-server","-conf","/gsnova/server.json"]

EXPOSE 8080 8088


