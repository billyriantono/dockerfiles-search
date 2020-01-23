FROM ubuntu:16.04

LABEL maintainer ysyou <youyongsong@gmail.com>

RUN apt-get update \
    && apt-get install -y wget vim.tiny curl zip make \
    && rm -rf /var/lib/apt/lists/*

RUN apt-get update \
    && apt-get install -y git jq cloc tree mosh \
    && rm -rf /var/lib/apt/lists/*

RUN curl -s https://packagecloud.io/install/repositories/github/git-lfs/script.deb.sh | bash \
    && apt-get install git-lfs \
    && git lfs install

RUN wget https://github.com/jingweno/ccat/releases/download/v1.1.0/linux-amd64-1.1.0.tar.gz \
    && tar -xzvf linux-amd64-1.1.0.tar.gz \
    && mv linux-amd64-1.1.0/ccat /usr/bin/ \
    && rm -r linux-amd64-1.1.0 && rm linux-amd64-1.1.0.tar.gz

COPY diff-so-fancy /usr/bin

COPY gitconfig /root/.gitconfig
COPY gitignore_global /root/.gitignore_global
RUN chmod +x /usr/bin/diff-so-fancy

ENTRYPOINT ["bash"]