FROM alpine:3.10
RUN apk update
RUN apk add curl \
            net-tools \
            nmap \
            bash \
            unzip

# Install Kubectl CLI
RUN curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.16.0/bin/linux/amd64/kubectl && \
    chmod +x ./kubectl && \
    mv ./kubectl /usr/local/bin/kubectl

# Install Openshift OC CLI
RUN curl -LO https://mirror.openshift.com/pub/openshift-v4/clients/oc/4.2/linux/oc.tar.gz && \
    tar -zxvf oc.tar.gz && \ 
    mv oc /usr/local/bin/oc

RUN curl -LO https://releases.hashicorp.com/vault/1.3.1/vault_1.3.1_linux_amd64.zip && \
    unzip vault_1.3.1_linux_amd64.zip && \
    mv ./vault /usr/local/bin/vault