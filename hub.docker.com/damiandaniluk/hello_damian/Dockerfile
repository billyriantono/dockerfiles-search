FROM alpine:latest

RUN apk update && \
    apk upgrade && \
    apk add python3

RUN mkdir /www
COPY index.html /www


EXPOSE 80

WORKDIR /www
CMD python3 -m http.server 80
