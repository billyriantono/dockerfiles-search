FROM rust:1.38 AS build

RUN \
    rustup target add wasm32-unknown-unknown; \
    cargo install cargo-web

WORKDIR /usr/src/resolutions-frontend

COPY Cargo.toml Cargo.lock ./
COPY src ./src
COPY static ./static

RUN cargo web deploy --release --output /var/www

FROM nginx
COPY --from=build /var/www /usr/share/nginx/html
