FROM ekidd/rust-musl-builder as build
ADD . /home/rust/src
WORKDIR /home/rust/src
RUN cargo build --release

FROM scratch
COPY --from=build /home/rust/src/target/x86_64-unknown-linux-musl/release/actixtest /
EXPOSE 3000

CMD ["/actixtest"]
