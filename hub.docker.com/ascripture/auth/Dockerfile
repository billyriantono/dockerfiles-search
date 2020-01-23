FROM rust:latest as builder
RUN apt-get update && apt-get -y install ca-certificates cmake musl-tools libssl-dev && rm -rf /var/lib/apt/lists/*
COPY . .
RUN cargo build --release

FROM debian:jessie-slim
RUN apt-get update
RUN apt-get -y install libpq-dev
COPY --from=builder /target/release/auth-rs .

CMD ["./auth-rs"]
EXPOSE 8088