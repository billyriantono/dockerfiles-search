FROM rust:1.40.0 as builder

RUN apt-get update && apt-get install -y musl-tools

RUN rustup target add x86_64-unknown-linux-musl

WORKDIR /usr/src/fayton
COPY . .
RUN cargo build --target x86_64-unknown-linux-musl --release

FROM scratch
COPY --from=builder /usr/src/fayton/target/x86_64-unknown-linux-musl/release/fayton /fayton
ENTRYPOINT [ "/fayton" ]

EXPOSE 8080