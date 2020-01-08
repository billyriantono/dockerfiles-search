FROM debian:buster-slim
LABEL maintainer="Martin Smola"

ENV DEBIAN_FRONTEND noninteractive

# Install dependencies.
RUN apt-get update \
    && apt-get -y full-upgrade \
    && apt-get install -y --no-install-recommends \
       sudo systemd systemd-sysv apt-utils \
       python-pip python-setuptools ansible nano curl \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /var/cache/* \    
    && rm -Rf /usr/share/doc && rm -Rf /usr/share/man \
    && apt-get clean

VOLUME ["/sys/fs/cgroup"]
CMD ["/lib/systemd/systemd"]
