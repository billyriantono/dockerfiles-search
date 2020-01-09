FROM matrixdotorg/synapse:v1.0.0-py3

MAINTAINER Alexander Olofsson <ace@haxalot.com>

RUN apk add git \
    && rm -rf /usr/local/lib/python3.6/site-packages/synapse \
    && git clone https://github.com/matrix-org/synapse.git /tmp/synapse \
    && git -C /tmp/synapse checkout develop \
    && mv /tmp/synapse/synapse /usr/local/lib/python3.6/site-packages/synapse \
    && set -eux \
    && mkdir -p /synapse/config /synapse/data /synapse/keys /synapse/tls \
    && addgroup -Sg 666 synapse \
    && adduser -Su 666 -G synapse -h /synapse/config -DH synapse \
    && echo "@edge http://nl.alpinelinux.org/alpine/edge/main" >> /etc/apk/repositories \
    && echo "@edgecommunity http://nl.alpinelinux.org/alpine/edge/community" >> /etc/apk/repositories \
    && apk add xmlsec@edge xmlsec-dev@edgecommunity \
    && wget https://github.com/devture/matrix-synapse-shared-secret-auth/raw/master/shared_secret_authenticator.py \
        -O /usr/local/lib/python3.6/site-packages/shared_secret_authenticator.py

ADD log.yaml /synapse
ADD matrix-synapse.sh /matrix-synapse
VOLUME /synapse/config /synapse/data /synapse/keys /synapse/tls

RUN chown -R synapse:synapse /synapse/config /synapse/data /synapse/keys /synapse/tls

EXPOSE 8008 8448
ENTRYPOINT [ "/matrix-synapse" ]
