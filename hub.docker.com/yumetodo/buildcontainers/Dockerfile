FROM rust
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash - && apt-get install -y nodejs && rm -rf /var/lib/apt/lists/* && \
        curl https://rustwasm.github.io/wasm-pack/installer/init.sh -sSf | sh
