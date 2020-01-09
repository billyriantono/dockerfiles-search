FROM alpine:3.8
MAINTAINER Karsten Kaj Jakobsen <kj@patientsky.com>

ARG BRANCH="none"
ARG COMMIT="local-build"
ARG BUILD_DATE="1970-01-01T00:00:00Z"
ARG URL="https://bitbucket.org/krugercorp/terraform-docker"
ARG VERSION="dirty"

ENV TERRAFORM_VERSION "0.11.8"
ENV TERRAFORM_PROVIDER_DIR "/opt"
ENV TERRAFORM_PROVIDER_VSPHERE_VERSION "1.8.0"
ENV TERRAFORM_PROVIDER_NULL_VERSION "1.0.0"
ENV TERRAFORM_PROVIDER_TEMPLATE_VERSION "1.0.0"
ENV TERRAFORM_PROVIDER_IGNITION_VERSION "1.0.1"
ENV TERRAFORM_PROVIDER_EXTERNAL_VERSION "1.0.0"

RUN apk add --update \
    wget \
    ca-certificates \
    unzip \
    git bash \
    cdrkit \
    qemu-img \
    openssh \
    jq

# Get latest Terraform bin
RUN wget -q -O /terraform.zip "https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/terraform_${TERRAFORM_VERSION}_linux_amd64.zip"

RUN unzip /terraform.zip -d /bin && \
    apk del --purge wget ca-certificates unzip && \
    rm -rf /var/cache/apk/* /terraform.zip

WORKDIR $TERRAFORM_PROVIDER_DIR

# Adding signature files
RUN mkdir -p /etc/terraform-docker
RUN echo $BRANCH > /etc/terraform-docker/branch
RUN echo $COMMIT > /etc/terraform-docker/commit
RUN echo $BUILD_DATE > /etc/terraform-docker/build_date
RUN echo $URL > /etc/terraform-docker/url
RUN echo $VERSION > /etc/terraform-docker/version

RUN wget -q "https://releases.hashicorp.com/terraform-provider-vsphere/${TERRAFORM_PROVIDER_VSPHERE_VERSION}/terraform-provider-vsphere_${TERRAFORM_PROVIDER_VSPHERE_VERSION}_linux_amd64.zip" && unzip -q terraform-provider-vsphere_${TERRAFORM_PROVIDER_VSPHERE_VERSION}_linux_amd64.zip
RUN wget -q "https://releases.hashicorp.com/terraform-provider-null/${TERRAFORM_PROVIDER_NULL_VERSION}/terraform-provider-null_${TERRAFORM_PROVIDER_NULL_VERSION}_linux_amd64.zip" && unzip -q terraform-provider-null_${TERRAFORM_PROVIDER_NULL_VERSION}_linux_amd64.zip
RUN wget -q "https://releases.hashicorp.com/terraform-provider-template/${TERRAFORM_PROVIDER_TEMPLATE_VERSION}/terraform-provider-template_${TERRAFORM_PROVIDER_TEMPLATE_VERSION}_linux_amd64.zip" && unzip -q terraform-provider-template_${TERRAFORM_PROVIDER_TEMPLATE_VERSION}_linux_amd64.zip
RUN wget -q "https://releases.hashicorp.com/terraform-provider-ignition/${TERRAFORM_PROVIDER_IGNITION_VERSION}/terraform-provider-ignition_${TERRAFORM_PROVIDER_IGNITION_VERSION}_linux_amd64.zip" && unzip -q terraform-provider-ignition_${TERRAFORM_PROVIDER_IGNITION_VERSION}_linux_amd64.zip
RUN wget -q "https://releases.hashicorp.com/terraform-provider-external/${TERRAFORM_PROVIDER_EXTERNAL_VERSION}/terraform-provider-external_${TERRAFORM_PROVIDER_EXTERNAL_VERSION}_linux_amd64.zip" && unzip -q terraform-provider-external_${TERRAFORM_PROVIDER_EXTERNAL_VERSION}_linux_amd64.zip

VOLUME ["/data"]

# Plugins can be provided along with the configuration by creating a terraform.d/plugins/OS_ARCH directory,
# which will be searched before automatically downloading additional plugins.
# The -get-plugins=false flag can be used to prevent Terraform from automatically downloading additional plugins.
RUN mkdir -p /root/.terraform.d/plugins/linux_amd64
WORKDIR /root/.terraform.d/plugins/linux_amd64

RUN cp $TERRAFORM_PROVIDER_DIR/* .

WORKDIR /data

ENTRYPOINT ["/bin/terraform"]

CMD ["--help"]
