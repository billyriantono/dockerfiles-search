FROM frolvlad/alpine-mono

WORKDIR /root

RUN apk add --no-cache openssl \
    && wget https://github.com/ionide/FsInteractiveService/releases/download/0.2.0/fsinteractiveservice.zip \
    && unzip fsinteractiveservice.zip \
    && rm fsinteractiveservice.zip

EXPOSE 8707

ENTRYPOINT [ "mono", "FsInteractiveService.exe", "0.0.0.0:8707" ]
