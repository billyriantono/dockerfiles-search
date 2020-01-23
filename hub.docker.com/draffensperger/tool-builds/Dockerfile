FROM draffensperger/docker-builds:util as util

# Rust nightly build on 2018-02-25
FROM rustlang/rust@sha256:65a46fe90f74bdf74e1eac1e3d8c150baf57ebb25a3ae373b7f72d740ed6e9d4

WORKDIR /root
COPY --from=util /util.sh .
ADD build-rg.sh .
RUN bash build-rg.sh
