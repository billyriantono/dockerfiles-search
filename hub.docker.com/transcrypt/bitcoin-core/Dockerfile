FROM alpine

LABEL maintainer="Anton Kulikov (anton.kulikov@tsrpay.com)"

RUN set -ex \
  && apk --no-cache add su-exec

ARG BITCOIN_VERSION=0.18.0
ARG BITCOIN_DIR=bitcoin-${BITCOIN_VERSION}
ARG BITCOIN_DIST=bitcoin-${BITCOIN_VERSION}-x86_64-linux-gnu.tar.gz
ARG BITCOIN_SHA256=5146ac5310133fbb01439666131588006543ab5364435b748ddfc95a8cb8d63f
ARG BITCOIN_SHASUM="${BITCOIN_SHA256}  ${BITCOIN_DIST}"
ARG BITCOIN_DATA=/home/bitcoin/.bitcoin

RUN wget -O ${BITCOIN_DIST} https://bitcoincore.org/bin/bitcoin-core-${BITCOIN_VERSION}/${BITCOIN_DIST} \
  && echo "${BITCOIN_SHASUM}" | sha256sum -c \
  && tar -xzf ${BITCOIN_DIST} \
  && mv ${BITCOIN_DIR}/bin/bitcoind ${BITCOIN_DIR}/bin/bitcoin-cli ${BITCOIN_DIR}/bin/bitcoin-tx /usr/local/bin/ \
  && rm -r ${BITCOIN_DIR} \
  && rm ${BITCOIN_DIST} \
  && addgroup -S bitcoin && adduser -S -G bitcoin bitcoin

# Install glibc binaries needed by bitcoin-abc
RUN apk --no-cache --allow-untrusted -X https://apkproxy.herokuapp.com/sgerrand/alpine-pkg-glibc add glibc glibc-bin

COPY docker-entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

VOLUME ["/home/bitcoin/.bitcoin"]

EXPOSE 8332 8333 18332 18333 18444

ENTRYPOINT ["/entrypoint.sh"]

CMD ["bitcoind"]
