FROM clux/muslrust:stable as builder

COPY . /workspace
RUN set -x \
  && cd /workspace \
  && cargo build --release \
  && mv /workspace/target/*/release /out

FROM scratch
COPY --from=builder /out/rust-ci-example /app

ENTRYPOINT ["/app"]

