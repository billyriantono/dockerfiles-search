FROM alpine:3.9 as builder

ARG VERSION='v1.14.0'

RUN apk add --no-cache --virtual .build-deps \
	build-base cmake boost-dev openssl-dev \
	mariadb-connector-c-dev git \
    && git clone --branch=${VERSION} https://github.com/trojan-gfw/trojan.git \
    && cd trojan && cmake . && make -j $(nproc) && strip -s trojan


FROM alpine:3.9

COPY --from=builder /trojan  /trojan
ADD run.sh /run.sh

RUN apk add boost-system boost-program_options \
	mariadb-connector-c libstdc++ bash jq \
    && mkdir /config \
    && chmod 755 /run.sh

ENTRYPOINT ["/run.sh"]
