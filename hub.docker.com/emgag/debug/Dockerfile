FROM debian:stretch-slim
LABEL maintainer="Matthias Blaser <mb@emgag.com>"

RUN apt-get update && apt-get install -y \
        curl \
        dnsutils \
        git \
        gnupg \
        httpie \
        iputils-arping \
        iputils-ping \
        ldnsutils \
        openssh-client \
        openssl \
        procps \
        strace \
        swaks \
        unzip \
    && apt-get clean \
    && apt-get autoremove -y \
    && rm -rf /var/lib/apt/lists/*