FROM azuresdk/azure-cli-python:2.0.21

LABEL authors="Artur Stolear <artur.stolear@gmail.com>"

ENV KUBERNETES_VERSION=1.8.4
RUN wget https://storage.googleapis.com/kubernetes-release/release/v${KUBERNETES_VERSION}/bin/linux/amd64/kubectl -qO /usr/local/bin/kubectl
RUN chmod +x /usr/local/bin/kubectl