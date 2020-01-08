FROM python:3-alpine 
MAINTAINER Matias Carrasco Kind <mgckind@gmail.com>
RUN pip install kubernetes && \
    apk add --update ca-certificates && \
    apk add --update -t deps curl && \
    apk add --no-cache tini && \
    curl -L https://storage.googleapis.com/kubernetes-release/release/v1.10.2/bin/linux/amd64/kubectl -o /usr/local/bin/kubectl && \
    chmod +x /usr/local/bin/kubectl && \
    apk del --purge deps && \
    rm -rf /var/cache/apk/*
ENTRYPOINT ["/sbin/tini", "--"]
