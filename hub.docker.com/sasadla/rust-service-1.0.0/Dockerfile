
FROM rustlang/rust:nightly

WORKDIR /usr/src/app
COPY . .

CMD ["rustup default nightly"]

CMD ["rustup override set nightly"]

CMD ["rustup update && cargo update"]

RUN cargo install

CMD ["rust_service"]
