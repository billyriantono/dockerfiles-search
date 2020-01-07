FROM frolvlad/alpine-glibc
# FROM alpine:latest
WORKDIR /gogen
RUN apk update && apk add \
    ca-certificates \
    openssl \
    wget
RUN wget https://api.gogen.io/linux/gogen --no-check-certificate
RUN chmod 755 ./gogen
ENTRYPOINT ["/gogen/gogen"]
CMD ["--help"]
