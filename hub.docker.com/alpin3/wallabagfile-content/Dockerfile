FROM docker:stable

RUN apk add --update ca-certificates \
 && apk add --update -t deps curl  \
 && apk add --update openssh gettext tar gzip \
 && apk add --no-cache python py-pip git bash gawk curl bash openssl \
 && apk add --no-cache -X http://dl-cdn.alpinelinux.org/alpine/edge/testing git-secret \
 && curl -sSL https://sdk.cloud.google.com | bash \
 && curl -L https://storage.googleapis.com/kubernetes-release/release/v1.15.3/bin/linux/amd64/kubectl -o /usr/local/bin/kubectl \
 && curl https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 | bash \
 && curl -L https://storage.googleapis.com/kubernetes-helm/helm-v2.16.1-linux-amd64.tar.gz | tar xz && mv linux-amd64/helm /bin/helm2 && rm -rf linux-amd64 \
 && chmod +x /usr/local/bin/kubectl \
 && apk del --purge deps \
 && rm /var/cache/apk/*

ENV PATH $PATH:/root/google-cloud-sdk/bin
