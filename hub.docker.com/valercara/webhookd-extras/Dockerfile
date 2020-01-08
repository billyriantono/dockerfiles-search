FROM ncarlier/webhookd:v1.6.0

ADD https://storage.googleapis.com/kubernetes-release/release/v1.12.0/bin/linux/amd64/kubectl /usr/bin/kubectl
RUN chmod +x /usr/bin/kubectl

RUN apk add --no-cache jq

