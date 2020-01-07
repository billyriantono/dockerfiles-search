FROM rust as build
WORKDIR /app
COPY . .
RUN cargo build --release

FROM rust
WORKDIR /app
EXPOSE 3000
COPY --from=build /app/target/release/hyperdemo /app/hyperdemo
ENTRYPOINT [ "./hyperdemo" ]
