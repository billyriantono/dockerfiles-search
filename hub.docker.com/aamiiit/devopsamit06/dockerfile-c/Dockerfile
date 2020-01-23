FROM ekidd/rust-musl-builder AS build-stage
RUN sh -c 'git clone https://github.com/jakedeichert/mask.git && cd mask && cargo build --release'

FROM scratch
COPY --from=build-stage /home/rust/src/mask/target/x86_64-unknown-linux-musl/release/mask /mask
