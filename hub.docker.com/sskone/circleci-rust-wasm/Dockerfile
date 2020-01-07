FROM circleci/rust

RUN curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -
RUN sudo apt-get install -y nodejs

RUN cargo install wasm-pack
RUN cargo install wasm-bindgen-cli
RUN cargo install cargo-generate
RUN cargo install cargo-release
RUN sudo npm install npm@latest -g

CMD ["/bin/sh"]
