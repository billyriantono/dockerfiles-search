FROM calvintam236/ubuntu:cuda

LABEL maintainer="calvintam236"
LABEL description="EWBF-Miner in Docker. Supports GPU mining."

WORKDIR /tmp

COPY ["EWBF_Equihash_miner_v0.6.tar.gz", "."]

RUN tar -xvf "EWBF_Equihash_miner_v0.6.tar.gz" \
    && rm "EWBF_Equihash_miner_v0.6.tar.gz" \
    && mv EWBF_Equihash_miner_v0.6/miner /usr/local/bin/ewbf-miner \
    && chmod a+x /usr/local/bin/ewbf-miner \
    && rm -r EWBF_Equihash_miner_v0.6 \
    && rm -rf /var/lib/{apt,dpkg,cache,log}

ENTRYPOINT ["ewbf-miner"]
CMD ["--help"]
