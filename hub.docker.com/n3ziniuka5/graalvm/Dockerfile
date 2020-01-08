FROM ubuntu:18.04

ENV GRAALVM_LINK https://github.com/oracle/graal/releases/download/vm-1.0.0-rc11/graalvm-ce-1.0.0-rc11-linux-amd64.tar.gz
RUN apt-get update && \
    apt-get install -y --no-install-recommends curl ca-certificates && \
    apt-get dist-upgrade -y && \
    apt-get autoremove -y && \
    rm -rf /var/lib/apt/lists/*

RUN curl -o /tmp/graalvm.tar.gz -LS ${GRAALVM_LINK} && \
    tar -xf /tmp/graalvm.tar.gz -C /opt && \
    rm /tmp/graalvm.tar.gz && \
    mv /opt/* /opt/graalvm

ENV PATH="/opt/graalvm/bin:${PATH}"
