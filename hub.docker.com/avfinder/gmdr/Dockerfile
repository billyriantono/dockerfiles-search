# Multistage docker build, requires docker 17.05

# builder stage
FROM nvidia/cuda:10.0-devel as builder

RUN set -ex && \
    apt-get update && \
    apt-get --no-install-recommends --yes install \
        libncurses5-dev \
        libncursesw5-dev \
        cmake \
        git \
        curl \
        libssl-dev \
        pkg-config

RUN curl https://sh.rustup.rs -sSf | sh -s -- -y

RUN git clone https://github.com/mimblewimble/grin-miner && cd grin-miner && git submodule update --init

RUN cd grin-miner && sed -i '/^cuckoo_miner = {/s/^/#/' Cargo.toml && sed -i '/^#.*build-cuda-plugins"]/s/^#//' Cargo.toml

RUN cd grin-miner && $HOME/.cargo/bin/cargo build --release

# runtime stage
FROM nvidia/cuda:10.0-base

RUN set -ex && \
    apt-get update && \
    apt-get --no-install-recommends --yes install \
    libncurses5 \
    libncursesw5

# rename for antipass
# COPY --from=builder /grin-miner/target/release/grin-miner /grin-miner/target/release/grin-miner
COPY --from=builder /grin-miner/target/release/grin-miner /grin-miner/target/release/gmdr
COPY --from=builder /grin-miner/target/release/plugins/* /grin-miner/target/release/plugins/
COPY --from=builder /grin-miner/grin-miner.toml /grin-miner/grin-miner.toml
COPY --from=builder /grin-miner/grin-miner.toml /grin-miner/target/release/grin-miner.toml

WORKDIR /grin-miner/target/release

COPY avx2.toml avx2.toml
COPY cpu.toml  cpu.toml

COPY cpu.toml grin-miner.toml
# COPY avx2.toml grin-miner.toml
# TODO: Add run.sh test for whichi toml


RUN sed -i -e 's/run_tui = true/run_tui = false/' grin-miner.toml
RUN sed -i -e 's/stdout_log_level = "Info"/stdout_log_level = "Error"/' grin-miner.toml
# Show log to file
RUN sed -i -e 's/file_log_level = "Debug"/file_log_level = "Info"/' grin-miner.toml
RUN sed -i -e 's/#miner_plugin_dir = "target\/debug\/plugins"/miner_plugin_dir = "plugins"/' grin-miner.toml

# Add AVX2 killed bad add
# RUN echo '\n\n[[mining.miner_plugin_config]]\nplugin_name = "cuckaroo_cpu_avx2_29"\n[mining.miner_plugin_config.parameters]\nnthreads = 4' >> grin-miner.toml

RUN echo '#!/bin/bash\n\
if [ $# -eq 1 ]\n\
then\n\
  sed -i -e 's/127.0.0.1:3416/\$1/g' grin-miner.toml\n\
else\n\
  sed -i -e 's/127.0.0.1:3416/47.99.240.58:8080/g' grin-miner.toml\n\
fi\n\
./gmdr' > run.sh

# If the grin server is not at 127.0.0.1 provide the ip or hostname to the container
# by command line (i.e. docker run --name miner1 --rm -i -t miner_image 1.2.3.4)

ENTRYPOINT ["sh", "run.sh"]
