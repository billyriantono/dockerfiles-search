FROM flyinprogrammer/terraform:latest
MAINTAINER Alan Scherger <flyinprogrammer@gmail.com>

ENV TERRAGRUNT_VERSION=v0.9.9
ADD https://github.com/gruntwork-io/terragrunt/releases/download/${TERRAGRUNT_VERSION}/terragrunt_linux_amd64 /bin/terragrunt
RUN chmod +x /bin/terragrunt

ENTRYPOINT ["/bin/terragrunt"]
