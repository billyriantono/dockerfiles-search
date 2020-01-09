FROM hashicorp/terraform:0.11.7

# RUN "mkdir -p .terraform.d/plugins/"

ENV TF_DATA_DIR "/.terraform"
COPY plugin_cache.tf /tmp/
RUN cd /tmp && terraform init

ENV TF_INPUT 0
