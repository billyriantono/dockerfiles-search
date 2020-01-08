# https://hub.docker.com/r/_/maven/
FROM maven:3.6.0-jdk-8-alpine

LABEL maintainer "29ygq@sina.com"

ENV KUBE_VERSION="v1.12.1" 

# https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl
RUN curl https://storage.googleapis.com/kubernetes-release/release/${KUBE_VERSION}/bin/linux/amd64/kubectl -o /usr/local/bin/kubectl \
  && chmod +x /usr/local/bin/kubectl

ENTRYPOINT ["/usr/local/bin/mvn-entrypoint.sh"]
CMD ["mvn"]
