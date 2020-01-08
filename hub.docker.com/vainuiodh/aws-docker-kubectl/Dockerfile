FROM docker:latest

RUN apk update && apk --no-cache add gettext ca-certificates openssl python py-pip
RUN pip install --no-cache-dir awscli
RUN wget https://storage.googleapis.com/kubernetes-release/release/v1.11.4/bin/linux/amd64/kubectl -O /usr/local/bin/kubectl && chmod a+x /usr/local/bin/kubectl
