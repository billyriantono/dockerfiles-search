FROM alpine:3.9

# Install glibc
ENV GLIBC_VERSION 2.29-r0
RUN set -ex \
  && wget -O /etc/apk/keys/sgerrand.rsa.pub https://alpine-pkgs.sgerrand.com/sgerrand.rsa.pub \
  && wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/${GLIBC_VERSION}/glibc-${GLIBC_VERSION}.apk \
  && apk add glibc-${GLIBC_VERSION}.apk \
  && rm glibc-${GLIBC_VERSION}.apk

# Install nomad
ENV NOMAD_VERSION 0.8.7
RUN set -ex \
  && apk add --no-cache --virtual .install-deps gnupg \
  && key=91A6E7F85D05C65630BEF18951852D87348FFC4C \
  && ( \
    gpg --batch --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-keys "$key" \
    || gpg --batch --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys "$key" \
    || gpg --batch --keyserver hkp://pgp.mit.edu:80 --recv-keys "$key" \
  ) \
  && wget https://releases.hashicorp.com/nomad/${NOMAD_VERSION}/nomad_${NOMAD_VERSION}_linux_amd64.zip \
  && wget https://releases.hashicorp.com/nomad/${NOMAD_VERSION}/nomad_${NOMAD_VERSION}_SHA256SUMS \
  && wget https://releases.hashicorp.com/nomad/${NOMAD_VERSION}/nomad_${NOMAD_VERSION}_SHA256SUMS.sig \
  && gpg --batch --verify nomad_${NOMAD_VERSION}_SHA256SUMS.sig nomad_${NOMAD_VERSION}_SHA256SUMS \
  && grep nomad_${NOMAD_VERSION}_linux_amd64.zip nomad_${NOMAD_VERSION}_SHA256SUMS | sha256sum -c \
  && unzip -d /usr/local/bin nomad_${NOMAD_VERSION}_linux_amd64.zip \
  && apk del .install-deps \
  && rm -rf nomad* /root/.gnupg

ENTRYPOINT ["nomad"]
