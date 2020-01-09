
FROM alpine:3.8

RUN apk add --no-cache curl

RUN mkdir /lib64 && ln -s /lib/libc.musl-x86_64.so.1 /lib64/ld-linux-x86-64.so.2

WORKDIR /app

RUN curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.16.3/bin/linux/amd64/kubectl
RUN chmod +x ./kubectl
RUN mv ./kubectl /usr/local/bin/kubectl
RUN curl -L https://github.com/digitalocean/doctl/releases/download/v1.33.1/doctl-1.33.1-linux-amd64.tar.gz | tar xz
RUN chmod +x ./doctl
RUN mv ./doctl /usr/local/bin/doctl
RUN curl -L https://get.helm.sh/helm-v3.0.0-rc.4-linux-amd64.tar.gz  | tar xz
RUN chmod +x ./linux-amd64/helm
RUN mv ./linux-amd64/helm /usr/local/bin/helm

ENTRYPOINT ["doctl"]