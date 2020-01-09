FROM ubuntu:18.04

    # Install Ruby and Mailcatcher build requirements
RUN apt-get update --yes --quiet && apt-get install --yes --no-install-recommends build-essential libsqlite3-0 libsqlite3-dev ruby ruby-dev && \
    # Install mailcatcher
    gem install mailcatcher --version 0.6.5 && \
    # Clean up build requirements
    apt-get --yes --purge autoremove build-essential libsqlite3-dev ruby-dev && \
    # Cleanup up apt caches
    apt-get clean --yes && \
    rm --recursive --force /var/lib/apt/lists/*

EXPOSE 1025
EXPOSE 1080

CMD ["mailcatcher", "--foreground", "--smtp-ip", "0.0.0.0", "--smtp-port", "1025", "--http-ip", "0.0.0.0", "--http-port", "1080"]
