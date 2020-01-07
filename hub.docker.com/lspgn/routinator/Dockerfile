FROM library/rust

RUN apt-get update && \
    apt-get install -y rsync && \
    cargo install routinator

ENTRYPOINT [ "routinator" ]
