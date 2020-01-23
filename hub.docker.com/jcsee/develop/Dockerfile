FROM ubuntu:17.04
ENV DEBIAN_FRONTEND=noninteractive \
    USERNAME=aaa \
    HOME=/home/aaa

RUN apt-get update \
 && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
      bash-completion \
      build-essential \
      cmake \
      git \
      less \
      man \
      python3 \
      rsync \
      ruby \
      ssh-client \
      sudo \
      tmux \
      vim \
 && rm -rf /var/lib/apt/lists/* \
 && useradd --uid 1000 --groups dialout --shell /bin/bash --no-create-home --home-dir $HOME $USERNAME

COPY entrypoint /entrypoint
ENTRYPOINT /entrypoint
