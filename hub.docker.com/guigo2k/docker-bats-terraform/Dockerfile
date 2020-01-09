FROM alpine:3.10

ENV TF_VERSION=0.12.7

# System requirements
RUN apk --update add bash curl git jq

# Install bats-core
RUN git clone https://github.com/bats-core/bats-core.git && \
    cd bats-core && \
    ./install.sh /usr/local

# Install tfenv
RUN git clone https://github.com/tfutils/tfenv.git ~/.tfenv && \
    ln -s ~/.tfenv/bin/* /usr/local/bin/ && \
    tfenv install $TF_VERSION
