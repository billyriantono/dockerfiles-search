FROM vapor/vapor:latest

ENV WORKDIR /vapor

ENV PORT 8000

WORKDIR $WORKDIR

ADD . $WORKDIR

RUN apt-get update &&  apt-get install -y openssl libssl-dev  --no-install-recommends && \
    vapor build && \
    apt-get remove -y libssl-dev && \
    rm -rf /var/lib/apt/lists/*

EXPOSE $PORT

