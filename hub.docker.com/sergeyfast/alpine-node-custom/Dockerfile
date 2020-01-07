FROM node:10.15-alpine
RUN apk update
RUN apk add --no-cache \
    autoconf \
    automake \
    bash \
    ca-certificates \
    curl \
    g++ \
    gcc \
    git \
    lcms2-dev \
    libjpeg-turbo-dev \
    libpng-dev \
    make \
    openssh-client \
    wget --virtual build-deps \
  && wget -q -O /etc/apk/keys/sgerrand.rsa.pub https://alpine-pkgs.sgerrand.com/sgerrand.rsa.pub \
  && wget -q https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.28-r0/glibc-2.28-r0.apk \
  && apk add glibc-2.28-r0.apk \
  && rm -rf glibc-2.28-r0.apk
 
