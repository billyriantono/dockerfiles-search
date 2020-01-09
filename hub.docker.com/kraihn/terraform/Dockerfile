FROM alpine:3.6
ARG TERRAFORM_VERSION=0.10.8

RUN apk add --no-cache ca-certificates curl unzip \
    && curl "https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/terraform_${TERRAFORM_VERSION}_linux_amd64.zip" -o /tmp/terraform.zip \
    && unzip /tmp/terraform.zip -d /usr/local/bin/ \
    && apk del curl unzip

ENTRYPOINT ["terraform"]
CMD ["--help"]
