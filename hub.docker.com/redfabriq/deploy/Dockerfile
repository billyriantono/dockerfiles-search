FROM microsoft/azure-cli
LABEL maintainer="Yann Ponzoni - RedFarbiQ <yann.ponzoni@redfabriq.com>"

# Install kubectl
RUN az aks install-cli

# Install helm
RUN curl -L https://git.io/get_helm.sh | bash	\
 && helm init --client-only

# Install rancher-cli
RUN curl -L https://github.com/rancher/cli/releases/download/v2.2.0/rancher-linux-amd64-v2.2.0.tar.gz | tar xz \
 && mv -v rancher-v2.2.0/* /usr/local/bin/

