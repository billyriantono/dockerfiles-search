# Official Alpine image
#FROM alpine:3.8
FROM scratch

MAINTAINER Aasif Shaikh <acloudiator@gmail.com>

# Alpine 3.8 x86_64 - Mini Root Filesystem (alpine-minirootfs-3.8.0-x86_64.tar.gz)
# http://dl-cdn.alpinelinux.org/alpine/v3.8/releases/x86_64/alpine-minirootfs-3.8.0-x86_64.tar.gz
ADD alpine-minirootfs-3.8.0-x86_64.tar.gz /

# Install any needed packages specified in requirements.txt
RUN apk update \
    && apk add --no-cache easy-rsa

# Define environment variable
ENV TYPE EASYRSA

# Run easy-rsa when the container launches
#CMD ["python", "app.py"]