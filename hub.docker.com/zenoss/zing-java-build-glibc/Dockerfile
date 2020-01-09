FROM zenoss/zing-java-build:1.1

ARG GLIBC_VERSION=2.25-r0

# Remove libc6-compat
RUN apk del --no-cache libc6-compat

# Install glibc from sgerrand/alpine-pkg-glibc
RUN curl -sSL https://alpine-pkgs.sgerrand.com/sgerrand.rsa.pub > /etc/apk/keys/sgerrand.rsa.pub && \
    curl -sSL https://github.com/sgerrand/alpine-pkg-glibc/releases/download/${GLIBC_VERSION}/glibc-${GLIBC_VERSION}.apk > glibc-${GLIBC_VERSION}.apk && \
    apk add --no-cache glibc-${GLIBC_VERSION}.apk && \
    rm -f glibc-${GLIBC_VERSION}.apk