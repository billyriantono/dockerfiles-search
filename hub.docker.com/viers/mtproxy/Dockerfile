FROM ubuntu:latest as builder

# Clone MTProxy project on the particular commit and build it.
RUN apt-get update                                               && \
    apt-get install -y git build-essential libssl-dev zlib1g-dev && \
    mkdir /build && cd /build                                    && \
    git clone https://github.com/TelegramMessenger/MTProxy .     && \
    git reset --hard dc0c7f3de40530053189c572936ae4fd1567269b    && \
    make

FROM python:3-slim

# Install curl, remove temporary files.
RUN pip3 install --no-cache-dir --upgrade requests==2.19 && \
    apt-get update && apt-get install -y curl            && \
    apt-get autoremove -y                                && \
    apt-get clean                                        && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*        && \
    mkdir /server

# Take the mtproto server from the builder image and run it.
COPY --from=builder /build/objs/bin/* /server
COPY src /src
CMD ["/src/entry.sh"]
