FROM docker:git

# Install TLS certificats, and curl (always useful).
RUN apk add --no-cache ca-certificates curl

RUN apk add --update -t deps curl  \
    && apk add --update gettext tar gzip

RUN set -x && \
    # Install kubectl
    # https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-via-curl
    curl -Lo /usr/local/bin/kubectl https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl && \
    chmod a+rx /usr/local/bin/kubectl && \
    \
    # Install envsubst (part of gettext package).
    # (at least until we have https://github.com/kubernetes/kubernetes/issues/23896 )
    apk add --no-cache gettext && \
    \
    # Install Helm client (better replacement to envsubst).
    apk add --no-cache -t .deps openssl && \
    curl https://raw.githubusercontent.com/kubernetes/helm/master/scripts/get | sh - && \
    apk del --purge .deps && \
    \
    # Verify
    kubectl version --client && \
    helm version --client

# Default directory
WORKDIR /code

COPY entrypoint.sh /usr/local/bin/
ENTRYPOINT ["entrypoint.sh"]
