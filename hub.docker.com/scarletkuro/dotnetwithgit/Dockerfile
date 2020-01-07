FROM microsoft/dotnet:2.2-sdk

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        git \
        libgit2-dev \
        wget \
    && rm -rf /var/lib/apt/lists/*

RUN wget http://snapshot.debian.org/archive/debian/20130319T033933Z/pool/main/o/openssl/libssl1.0.0_1.0.1e-2_amd64.deb -O /tmp/libssl1.0.0_1.0.1e-2_amd64.deb && \
 dpkg -i /tmp/libssl1.0.0_1.0.1e-2_amd64.deb