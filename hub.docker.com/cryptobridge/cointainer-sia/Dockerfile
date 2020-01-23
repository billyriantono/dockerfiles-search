FROM cryptobridge/baseimage:bionic-build AS build
ENV VERSION 1.4.1.2

RUN mkdir -p /hs && \
    wget -O /tmp/install.zip https://siaprime.net/releases/ScPrime-v${VERSION}-linux-amd64.zip && \
    unzip -d /tmp/install/ /tmp/install.zip

FROM cryptobridge/baseimage:bionic
ENV VERSION 1.4.1.2

COPY --from=build /tmp/install/ScPrime-v${VERSION}-linux-amd64/spd /usr/local/bin/
COPY --from=build /tmp/install/ScPrime-v${VERSION}-linux-amd64/spc /usr/local/bin/

WORKDIR /sp
EXPOSE 4281 4282
USER crypto

CMD ["/usr/local/bin/spd"]
