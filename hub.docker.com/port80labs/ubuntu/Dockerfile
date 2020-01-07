FROM ubuntu:latest

# Install.
RUN \
  sed -i 's/# \(.*multiverse$\)/\1/g' /etc/apt/sources.list && \
  apt-get update && \
  apt-get -y upgrade && \
  apt-get install -y build-essential \
    curl \
    nano \
    python \
    language-pack-en \
    git && \
  apt-get remove -y man && \
  rm -rf /var/lib/apt/lists/*

RUN groupadd -r ubuntu && useradd -ms /bin/bash -g ubuntu ubuntu 
USER ubuntu
ENV HOME /home/ubuntu

# Define working directory.
WORKDIR /home/ubuntu

RUN git clone https://github.com/port80labs/dotfiles.git && \
  cp dotfiles/.* ./ || true &&\
  rm -rf dotfiles

# Define default command.
CMD ["bash"]
