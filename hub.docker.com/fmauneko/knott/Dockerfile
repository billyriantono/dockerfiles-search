FROM redis:5.0.5-alpine AS redis

FROM liuchong/rustup:nightly-musl

RUN curl -L https://github.com/mozilla/sccache/releases/download/0.2.12/sccache-0.2.12-x86_64-unknown-linux-musl.tar.gz | tar xvz -C /tmp \
    && mv /tmp/sccache-0.2.12-x86_64-unknown-linux-musl/sccache /usr/bin/sccache

ENV RUSTC_WRAPPER=/usr/bin/sccache

COPY entrypoint.sh /entrypoint.sh

COPY --from=redis /usr/local/bin/redis-server /usr/local/bin/redis-server

ENTRYPOINT ["/entrypoint.sh"]
