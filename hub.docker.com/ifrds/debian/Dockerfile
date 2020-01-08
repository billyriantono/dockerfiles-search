FROM debian:9
MAINTAINER Tomasz Tylec <ttylec@ifesearch.pl>

RUN apt-get update && \
    apt-get install --no-install-recommends -yq \
            openssh-client \
            python3 python3-pip python3-venv \
            make pandoc \
            rsync && \
    apt-get autoremove -y && \
    rm -rf /var/lib/apt/lists/*.deb
