FROM lachlanevenson/k8s-kubectl:v1.15.1

# Add Rancher CLI
ENV RANCHER_VER=v2.2.0

RUN apk add --update -t deps curl \
    && curl -L https://releases.rancher.com/cli2/$RANCHER_VER/rancher-linux-amd64-$RANCHER_VER.tar.gz -o rancher-linux-amd64-$RANCHER_VER.tar.gz \
    && tar -xvf rancher-linux-amd64-$RANCHER_VER.tar.gz \
    && cp rancher-$RANCHER_VER/rancher /usr/local/bin/rancher \
    && apk del --purge deps \
    && rm /var/cache/apk/*

ENTRYPOINT []
