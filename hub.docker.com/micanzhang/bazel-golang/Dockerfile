FROM ubuntu:16.04

RUN apt-get update && apt-get install -y --no-install-recommends \
        build-essential \
        curl \
        git \
        unzip \
        openssh-client \
        python=2.7.* \
        python-pip \
        openjdk-8-jdk \
        openjdk-8-jre-headless && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    pip --no-cache-dir install --upgrade pip && \
    pip --no-cache-dir install grpcio && \
    curl -L https://github.com/bazelbuild/bazel/releases/download/0.5.4/bazel-0.5.4-without-jdk-installer-linux-x86_64.sh \
        --output /tmp/bazel-installer.sh && \
    chmod +x /tmp/bazel-installer.sh && \
    bash /tmp/bazel-installer.sh && \
    rm /tmp/bazel-installer.sh && \
    curl -L https://golang.org/dl/go1.9.2.linux-amd64.tar.gz | tar zx -C /usr/lib && \
    touch /root/WORKSPACE

WORKDIR /root

CMD ["bin/bash"]
