FROM alpine:3.9

RUN set -ex \
&& apk --no-cache add su-exec

ENV BITCOIN_ABC_VERSION=0.20.6
ENV BITCOIN_ABC_DIR=bitcoin-abc-${BITCOIN_ABC_VERSION}
ENV BITCOIN_ABC_DIST=bitcoin-abc-${BITCOIN_ABC_VERSION}-x86_64-linux-gnu.tar.gz
ENV BITCOIN_ABC_SHASUM="f5fb4a3dac6164709dbf0632f64adfe56414d260e4bf192effc0049da9c43bac  ${BITCOIN_ABC_DIST}"
ENV BITCOIN_ABC_DATA=/home/bitcoin/.bitcoin

RUN wget -O $BITCOIN_ABC_DIST https://download.bitcoinabc.org/${BITCOIN_ABC_VERSION}/linux/${BITCOIN_ABC_DIST} \
&& echo "$BITCOIN_ABC_SHASUM" | sha256sum -c \
&& tar -xzf $BITCOIN_ABC_DIST \
&& mv ${BITCOIN_ABC_DIR}/bin/bitcoind ${BITCOIN_ABC_DIR}/bin/bitcoin-cli ${BITCOIN_ABC_DIR}/bin/bitcoin-tx /usr/local/bin/ \
&& rm -r $BITCOIN_ABC_DIR \
&& rm $BITCOIN_ABC_DIST \
&& addgroup -S bitcoin && adduser -S -G bitcoin bitcoin

# Install glibc binaries needed by bitcoin-abc
RUN apk --no-cache --allow-untrusted -X https://apkproxy.herokuapp.com/sgerrand/alpine-pkg-glibc add glibc glibc-bin

COPY docker-entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

VOLUME ["/home/bitcoin/.bitcoin"]

EXPOSE 8332 8333 18332 18333 18444

ENTRYPOINT ["/entrypoint.sh"]

CMD ["bitcoind"]
