FROM library/docker:stable

ENV TERRAFORM_VERSION=0.11.11
ENV ANSIBLE_VERSION=2.5.5-r0

RUN apk add unzip && \
    wget -O terraform-0.11.11.zip https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/terraform_${TERRAFORM_VERSION}_linux_amd64.zip && \
    unzip terraform-${TERRAFORM_VERSION}.zip -d /bin

RUN apk add ansible=${ANSIBLE_VERSION}
RUN apk add make
RUN apk add --no-cache openssh
RUN apk add git
