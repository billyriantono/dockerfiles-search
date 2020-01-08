FROM microsoft/azure-cli

# Install kubectl
RUN az acs kubernetes install-cli

# Install Helm
RUN curl https://raw.githubusercontent.com/kubernetes/helm/master/scripts/get | bash
RUN helm init --client-only
RUN helm plugin install https://github.com/chartmuseum/helm-push
