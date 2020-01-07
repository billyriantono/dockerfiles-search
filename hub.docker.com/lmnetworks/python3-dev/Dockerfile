FROM lmnetworks/python3:3.7.4_20191014

LABEL image_name="lmnetworks/python3-dev"
LABEL maintainer="info@lm-net.it"

# currently Alpine Linux v3.10 has Python-3.7 but no PyLint
# hadolint ignore=DL3013
RUN echo '@edge_testing http://dl-cdn.alpinelinux.org/alpine/edge/testing' >> /etc/apk/repositories && \
    apk add --no-cache py3-isort=4.3.19-r0 py3-pylint@edge_testing=2.4.2-r0 && \
    pip3 install wheel && \
    rm -rf /root/.cache /var/cache/apk/*
