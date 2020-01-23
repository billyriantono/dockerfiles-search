FROM alpine:latest

RUN apk add --update --no-cache curl ca-certificates

RUN curl -L -o /usr/local/bin/argocd https://github.com/argoproj/argo-cd/releases/download/v1.3.6/argocd-linux-amd64

RUN chmod +x /usr/local/bin/argocd

RUN apk del curl ca-certificates

RUN rm -f /var/cache/apk/*