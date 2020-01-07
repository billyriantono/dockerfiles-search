FROM docker:stable-dind

LABEL maintainer=joe@twr.io

RUN apk add --update --no-cache openrc bind-tools ca-certificates bash git curl

RUN curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
RUN chmod +x ./kubectl; mv ./kubectl /usr/local/bin/

RUN curl -LO https://github.com/kubernetes-sigs/kind/releases/download/v0.4.0/kind-linux-amd64 -o kind
RUN chmod +x ./kind*; mv ./kind* /usr/local/bin/kind

CMD ["dind", "dockerd"]
