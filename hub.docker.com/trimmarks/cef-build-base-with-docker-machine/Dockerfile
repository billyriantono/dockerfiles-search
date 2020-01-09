FROM trimmarks/cef-build-base:2.0
RUN set -x && \
    apt-get update && \
    apt-get install -y apt-transport-https ca-certificates curl software-properties-common && \
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add - && apt-key fingerprint 0EBFCD88 && \
    add-apt-repository -y "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" && \
    apt-get update && apt-get install -y docker-ce && \
    curl -L https://github.com/docker/machine/releases/download/v0.15.0/docker-machine-Linux-x86_64 >/usr/local/bin/docker-machine && \
    chmod +x /usr/local/bin/docker-machine

