FROM alpine:3.8
MAINTAINER Mike Barrett

COPY scripts/docker-stacker /bin/docker-stacker
WORKDIR /stacks
COPY . /tmp/stacker

RUN apk --no-cache update && \
    apk --no-cache add python2 py2-pip py-yaml build-base && \
    mkdir -p /stacks && \
    pip install --upgrade setuptools && \
    pip install yamllint && \
    cd /tmp/stacker && \
    python setup.py install && \
    rm -rf /tmp/stacker && \
    apk --no-cache del build-base && \
    rm -rf /var/cache/apk/*

ENTRYPOINT ["docker-stacker"]
CMD ["-h"]
