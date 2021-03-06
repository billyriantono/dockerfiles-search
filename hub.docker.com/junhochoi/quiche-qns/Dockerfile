# 
# quiche build image for quic-interop-runner
# https://github.com/marten-seemann/quic-network-simulator
# https://github.com/marten-seemann/quic-interop-runner
#

# build quiche binary
FROM martenseemann/quic-network-simulator-endpoint:latest AS builder

# dependencies
RUN apt-get update && apt-get install -y cmake golang git curl

# rust need to be installed via rustup since it requires 1.38
RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | \
    sh -s -- --default-toolchain stable -y
ENV PATH=/root/.cargo/bin:$PATH

# build quiche
RUN git clone --recursive https://github.com/cloudflare/quiche.git
WORKDIR /quiche
RUN cargo build --release --examples

# setup interop image
FROM martenseemann/quic-network-simulator-endpoint:latest

WORKDIR /quiche

# copy binaries and sample certificate for server
COPY --from=builder /quiche/examples/cert.crt examples/ 
COPY --from=builder /quiche/examples/cert.key examples/ 
COPY --from=builder /quiche/target/release/examples/client .
COPY --from=builder /quiche/target/release/examples/server .
COPY --from=builder /quiche/target/release/examples/http3-client .
COPY --from=builder /quiche/target/release/examples/http3-server .

# copy interop test script
COPY run_endpoint.sh .
RUN chmod +x run_endpoint.sh

ENTRYPOINT [ "./run_endpoint.sh" ]
