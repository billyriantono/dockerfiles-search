FROM debian:stretch-slim

MAINTAINER Ian Foster <ian@vorsk.com>

RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install --no-install-recommends -y vim git curl wget ca-certificates less && \
    apt-get clean && \ 
    rm -rf /var/lib/apt/lists/* 

RUN git clone --depth 1 https://github.com/lanrat/dotfiles.git /root/dotfiles && \
    /root/dotfiles/link.sh shell && \
    /root/dotfiles/link.sh scripts && \
    /root/dotfiles/link.sh vim

CMD bash
