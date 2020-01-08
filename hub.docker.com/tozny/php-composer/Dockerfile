FROM alpine:3.4

# Default to UTF-8 file.encoding
ENV LANG C.UTF-8

# add alpine testing repositories for composer@testing package
COPY repositories /etc/apk/repositories
# install for ses stuff
RUN apk add --no-cache php5 \
  composer@testing

ENTRYPOINT composer
