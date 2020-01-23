FROM cryptobridge/baseimage:bionic-build AS build

RUN git clone https://github.com/hydnoracoin/hora_geth.git . && git checkout v1.1
RUN chmod 755 ./build/env.sh
RUN make geth

FROM cryptobridge/baseimage:bionic

COPY --from=build /build/build/bin/geth /usr/local/bin/
EXPOSE 8548
USER crypto
CMD ["geth"]
