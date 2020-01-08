FROM ibmterraform/terraform-provider-ibm-docker:v0.20.0

ENV CALICO_CLI_VERSION v3.3.1
ENV KUBE_CLI_VERSION v1.13.7
ENV HELM_CLIENT_VERSION v2.14.3

WORKDIR /ibmtf

# setup the PV mount point - must match value of DEVOPS_TFBACKEND_MOUNT in the UCD application configuration
RUN echo "prepare" ; \
 mkdir -p /mnt/tfbackend ; \
 mkdir scripts ; \
 apk add jq openssh tar gzip docker gettext

COPY scripts/kubernetes scripts/
COPY scripts/registry scripts/
COPY scripts/terraform scripts/

###################################################################################################
# Get IBM Cloud CLI (Kubernetes Service CLI and Container Registry CLI)
# References:
#  https://console.bluemix.net/docs/cli/reference/ibmcloud/download_cli.html#install_use
#  https://console.bluemix.net/docs/cli/reference/ibmcloud/download_cli.html#shell_install
###################################################################################################
RUN chmod -R +x scripts/* ; \
 curl -fsSL https://plugins.cloud.ibm.com/install/linux | sh ; \
 ibmcloud update -f ; \
 ibmcloud plugin install container-service -r "IBM Cloud" ; \
 ibmcloud plugin install container-registry -r "IBM Cloud" ; \
 ibmcloud plugin install cloud-functions ; \
 ibmcloud plugin install cloud-object-storage ; \
 ibmcloud plugin install schematics; \
 ibmcloud plugin install cis -f
###################################################################################################
# Get Kubernetes CLI
# Reference:
#  Step # 4 at
#  https://console.bluemix.net/docs/containers/cs_cli_install.html#cs_cli_install_steps
# For the latest stable - you can use this
# RUN curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
###################################################################################################
### install helm client
RUN curl -LO https://storage.googleapis.com/kubernetes-release/release/${KUBE_CLI_VERSION}/bin/linux/amd64/kubectl ; \
 chmod a+x kubectl ; \
 mv kubectl /usr/local/bin ; \
 curl -L https://storage.googleapis.com/kubernetes-helm/helm-${HELM_CLIENT_VERSION}-linux-amd64.tar.gz | tar xz && mv linux-amd64/helm /bin/helm && rm -rf linux-amd64 ; \
 helm init --client-only

################################################################################################
# Get Calico CLI
# Reference:  https://console.bluemix.net/docs/containers/cs_network_policy.html#cli_install
################################################################################################
RUN curl -O -L https://github.com/projectcalico/calicoctl/releases/download/${CALICO_CLI_VERSION}/calicoctl ; \
 mv ./calicoctl /usr/local/bin/calicoctl ; \
 chmod +x /usr/local/bin/calicoctl ; \
 wget https://dl.min.io/client/mc/release/linux-amd64/mc ; \
 mv ./mc /usr/local/bin/mc ; \
 chmod +x /usr/local/bin/mc

#############################################################################
# Install npm and python  
############################################################################
RUN apk add --update nodejs nodejs-npm ; \
 apk add --update \
    python \
    python-dev \
    py-pip \
    build-base \
  && pip install virtualenv \
  && rm -rf /var/cache/apk/* ; \
  sh -c "curl https://raw.githubusercontent.com/mrowa44/emojify/master/emojify -o /usr/local/bin/emojify && chmod +x /usr/local/bin/emojify"


ENV PATH $PATH:/ibmtf/scripts/
