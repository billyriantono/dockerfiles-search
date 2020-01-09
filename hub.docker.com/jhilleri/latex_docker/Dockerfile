FROM rust:latest as builder 
RUN apt-get update && apt-get install -y libfontconfig1-dev libgraphite2-dev libharfbuzz-dev libicu-dev zlib1g-dev
RUN cargo install tectonic --force

WORKDIR /usr/src/tex
COPY ./exemple ./
RUN tectonic document.tex

FROM debian:stretch-slim
RUN apt-get update \
     && apt-get install -y --no-install-recommends libfontconfig1 libgraphite2-3 libharfbuzz0b libicu57 zlib1g libharfbuzz-icu0 libssl1.1 ca-certificates \
    && rm -rf /var/lib/apt/lists/* 
COPY --from=builder /usr/local/cargo/bin/tectonic /usr/bin/
COPY --from=builder /root/.cache/Tectonic/ /root/.cache/Tectonic/

VOLUME [ "/tex" ]
WORKDIR "/tex"
ENTRYPOINT [ "tectonic" ]