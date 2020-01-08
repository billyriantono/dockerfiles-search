FROM postgres:12

RUN apt-get update &&                       \
    apt-get install -y ca-certificates &&   \
    rm -rf /var/lib/apt/lists/* &&          \
    rm -rf /var/apt/cache/*
COPY DOIRootCA2.crt /usr/local/share/ca-certificates/
RUN update-ca-certificates

