FROM lachlanevenson/k8s-kubectl:v1.4.3

ENV HELM_LATEST_VERSION="v2.0.0-beta.1"

RUN apk add --update ca-certificates \
 && apk add --update -t deps curl \
 && curl -L http://storage.googleapis.com/kubernetes-helm/helm-${HELM_LATEST_VERSION}-linux-386.tar.gz  | tar -Oxzf - linux-386/helm > /usr/local/bin/helm \
 && chmod +x /usr/local/bin/helm \
 && apk del --purge deps \
 && rm /var/cache/apk/*

ENTRYPOINT ["helm"]
CMD ["help"]
