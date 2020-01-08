FROM node:alpine

LABEL \
    maintainer="Morgan AUCHEDE <morgan.auchede@gmail.com>"

ENV \
    CHOKIDAR_USEPOLLING=true

RUN set -e -u -x \
\
    # Install packages
\
    && apk add --no-cache --no-progress bash binutils ca-certificates curl g++ git gpgme make openssh-client python \
\
    # Install create-react-app
\
    && yarn global add create-react-app \
\
    # Install dumb-entrypoint
\
    && curl --location "https://gitlab.com/timonier/dumb-entrypoint/raw/master/src/dumb-entrypoint/installer" | bash -s -- install \
    && curl --location "https://gitlab.com/timonier/dumb-entrypoint/raw/master/src/gosu/installer" | bash -s -- install \
\
    # Install generate-api-platform-client
\
    && yarn global add @api-platform/client-generator \
\
    # Install glibc
\
    && export $(curl --location "https://gitlab.com/timonier/version-lister/raw/generated/sgerrand/alpine-pkg-glibc/latest" | xargs) \
    && curl --location --output /etc/apk/keys/sgerrand.rsa.pub "${GLIBC_REPOSITORY_KEY}" \
    && curl --location --output /tmp/glibc.apk "${GLIBC_PACKAGE}" \
    && curl --location --output /tmp/glibc-bin.apk "${GLIBC_BIN_PACKAGE}" \
    && apk add --no-cache --no-progress /tmp/glibc.apk /tmp/glibc-bin.apk \
\
    # Install ng
\
    && yarn global add @angular/cli \
\
    # Install prettier
\
    && yarn global add prettier \
\
    # Install serve
\
    && yarn global add serve \
\
    # Clean
\
    && rm -f -r /tmp/* "$(yarn cache dir)"/*

ENTRYPOINT [ "dumb-entrypoint" ]
