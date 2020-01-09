FROM azuresdk/azure-cli-python:2.0.23

LABEL authors="Jayakarthi D <jayakarthi.d@gmail.com>"

ENV KUBERNETES_VERSION=1.11.2
RUN wget https://storage.googleapis.com/kubernetes-release/release/v${KUBERNETES_VERSION}/bin/linux/amd64/kubectl -qO /usr/local/bin/kubectl
RUN chmod +x /usr/local/bin/kubectl
