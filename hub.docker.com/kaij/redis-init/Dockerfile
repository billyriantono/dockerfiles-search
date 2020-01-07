FROM redis:alpine

ENV KUBE_LATEST_VERSION="v1.14.3"

RUN apk add --update ca-certificates \
 && apk add --update -t deps curl \
 && curl -L https://storage.googleapis.com/kubernetes-release/release/$KUBE_LATEST_VERSION/kubernetes-client-linux-arm.tar.gz -o /usr/local/bin/kubectl \
 && chmod +x /usr/local/bin/kubectl \
 && apk del --purge deps \
 && rm /var/cache/apk/*
 
VOLUME /var/kubeconfigs/
 
ENTRYPOINT ["kubectl", "--config", "/var/kubeconfigs/config.conf", "exec", "-it", "redis-cluster-0", "--", "redis-cli", "--cluster", "create", "$(kubectl", "--config", "/var/kubeconfigs/config.conf", "get", "pods", "-l", "app=redis-cluster", "-o", "jsonpath='{range.items[*]}{.status.podIP}:6379 ')"]
CMD ["--cluster-replicas", "1"]