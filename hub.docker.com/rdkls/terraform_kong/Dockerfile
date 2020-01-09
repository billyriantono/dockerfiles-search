FROM hashicorp/terraform:light
ARG plugin_bin=terraform-provider-kong_1.5.0
ARG tf_provider_kong_zip=https://github.com/kevholditch/terraform-provider-kong/releases/download/v1.5.0/terraform-provider-kong_1.5.0_linux_amd64.zip

WORKDIR `mktemp`
ADD $tf_provider_kong_zip .
RUN unzip *zip
RUN rm *.md *zip 2>/dev/null
RUN mv * /bin

WORKDIR /opt/tf
