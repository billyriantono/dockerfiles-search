FROM alpine
ENV \
TERRAFORM_VERSION=0.8.4 \
TERRAGRUNT_VERSION=0.9.1

RUN apk --no-cache add --virtual build-dependencies curl unzip \
# ecs-cli
&& curl --location --silent https://s3.amazonaws.com/amazon-ecs-cli/ecs-cli-linux-amd64-latest -o /bin/ecs-cli \
&& echo $(curl --location --silent https://s3.amazonaws.com/amazon-ecs-cli/ecs-cli-linux-amd64-latest.md5)'  /bin/ecs-cli' | md5sum -c - \
# terraform
&& curl -sL https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/terraform_${TERRAFORM_VERSION}_linux_amd64.zip -o terraform_${TERRAFORM_VERSION}_linux_amd64.zip \
&& unzip terraform_${TERRAFORM_VERSION}_linux_amd64.zip -d /bin \
&& rm -f terraform_${TERRAFORM_VERSION}_linux_amd64.zip \
# terragrunt
&& curl -sL https://github.com/gruntwork-io/terragrunt/releases/download/v${TERRAGRUNT_VERSION}/terragrunt_linux_amd64 -o /bin/terragrunt \
#
&& apk del build-dependencies \
&& chmod +x /bin/terraform /bin/terragrunt /bin/ecs-cli
