ARG TERRAFORM_IMAGE_VERION=0.11.11
ARG GOLANG_IMAGE_VERSION=1.11.5-stretch
ARG HELM_IMAGE_VERSION=2.12.3

FROM hashicorp/terraform:${TERRAFORM_IMAGE_VERION} as terraform
FROM alpine/helm:${HELM_IMAGE_VERSION} as helm

FROM golang:${GOLANG_IMAGE_VERSION}

COPY --from=terraform /bin/terraform /bin/terraform
COPY --from=helm /usr/bin/helm /usr/bin/helm

ARG AZURE_CLI_VERSION=2.0.57

# Install mssql-tools
# Note: locales, forcing en_US.UTF-8 and localegen are required because of
# https://github.com/Microsoft/mssql-docker/issues/163
RUN apt-get update && apt-get install -y apt-transport-https locales  && rm -rf /var/lib/apt/lists/* && \
    echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen && locale-gen
COPY prod.list /etc/apt/sources.list.d/msprod.list
COPY ms-package-key /
RUN apt-key add /ms-package-key

RUN apt-get update && ACCEPT_EULA=Y apt-get -y install bash python-pip dumb-init git nodejs gcc libffi-dev musl-dev libssl-dev python-dev make mssql-tools jq && \
    pip --no-cache-dir install --upgrade pip && rm -rf /var/lib/apt/lists/* && \
    wget https://storage.googleapis.com/kubernetes-release/release/$(wget -qO - https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl && \
    mv kubectl /usr/bin && chmod +x /usr/bin/kubectl && ln -s /opt/mssql-tools/bin/sqlcmd /usr/bin/sqlcmd
# Remove pyOpenSSL: for terraform/azure the version included via pip is not correct and results in certificate errors:
#      AttributeError: 'module' object has no attribute 'X509_up_ref'
#      [...] Error detail: HTTPSConnectionPool(host='login.microsoftonline.com', port=443): Max retries exceeded with url: [...]
#                                     (Caused by SSLError(SSLError("bad handshake: Error([('SSL routines', 'tls_process_server_certificate', 'certificate verify failed')],)",),))
RUN pip --no-cache-dir install databricks-cli azure-cli==${AZURE_CLI_VERSION} && pip uninstall --yes pyOpenSSL && \
    helm init --client-only

# CGO requires a C compiler, which we do not need
ENV CGO_ENABLED=0
WORKDIR $GOPATH/src/app

COPY docker-entrypoint.sh /bin

ENTRYPOINT ["/usr/bin/dumb-init"]

CMD ["/bin/bash"]

