FROM docker:dind

ENV REGISTRY=registry.bestplayers.ru

COPY ca.crt /tmp/ca.crt
RUN install -D /tmp/ca.crt /etc/docker/certs.d/${REGISTRY}/ca.crt && \
    install -D /tmp/ca.crt /usr/local/share/ca-certificates/ca.crt && \
    cat /tmp/ca.crt >>/etc/ssl/certs/ca-certificates.crt && \
    rm /tmp/ca.crt