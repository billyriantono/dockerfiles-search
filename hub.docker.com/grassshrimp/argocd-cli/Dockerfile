FROM alpine AS builder
RUN apk update && \
    apk add curl && \
    curl -sSL -o /usr/local/bin/argocd https://github.com/argoproj/argo-cd/releases/download/v1.2.1/argocd-linux-amd64 && \
    chmod +x /usr/local/bin/argocd

FROM alpine:latest
COPY --from=builder /usr/local/bin/argocd /usr/local/bin/argocd
ENTRYPOINT /usr/local/bin/argocd
CMD ["--help"]