FROM debian:stretch

ENV DOCTL_VERSION 1.23.1

RUN apt-get update && apt-get install -y curl

# Install Kubectl
RUN curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl
RUN chmod +x ./kubectl
RUN mv ./kubectl /usr/local/bin/

# Install Doctl
RUN curl -L https://github.com/digitalocean/doctl/releases/download/v${DOCTL_VERSION}/doctl-${DOCTL_VERSION}-linux-amd64.tar.gz | tar xz
RUN chmod +x ./doctl
RUN mv ./doctl /usr/local/bin/

# Install Helm
RUN curl -LO https://git.io/get_helm.sh
RUN chmod a+x get_helm.sh
RUN ./get_helm.sh
