# Smallest base image
FROM alpine:latest

LABEL maintainer="Artur Scheiner <artur.scheiner@gmail.com>"

RUN mkdir -p /flee/bin && \
    apk add nodejs && \
    cd /flee/bin

ADD fleections /flee/bin
ADD FLEE_VERSION /flee/bin
ADD fleedec /flee/bin/fleedec
ADD oui.txt /flee/bin

WORKDIR /flee/bin
CMD ["/flee/bin/fleections"]
