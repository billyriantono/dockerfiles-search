FROM alpine:3.8

RUN build_deps="build-base libxml2-dev libxslt-dev python2-dev" && \
    apk add -U $build_deps make doxygen git libxml2 libxslt py2-pip && \
    pip install doc2dash breathe recommonmark && \
    apk del $build_deps && \
    rm -rf /root/.cache /var/cache/apk/*
