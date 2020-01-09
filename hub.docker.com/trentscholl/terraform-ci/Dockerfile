FROM hashicorp/terraform:0.11.7
LABEL Author="Trent Scholl <me@trentscholl.com>"

ENV TERRAGRUNT_VERSION=0.16.3
ENV TFLINT_VERSION=0.7.0

RUN curl -sL https://github.com/gruntwork-io/terragrunt/releases/download/v$TERRAGRUNT_VERSION/terragrunt_linux_386 \
  -o /bin/terragrunt && chmod +x /bin/terragrunt


RUN curl -sL https://github.com/wata727/tflint/releases/download/v$TFLINT_VERSION/tflint_linux_386.zip \
  -o tflint.zip && unzip tflint.zip -d /bin && chmod +x /bin/tflint

ENTRYPOINT ["/bin/terragrunt"]