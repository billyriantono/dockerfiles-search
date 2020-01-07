FROM alpine:latest
MAINTAINER "Joost van der Laan <joost@fashionunited.com>"

ENV TERRAFORM_VERSION=0.11.7
ENV TERRAFORM_FILENAME=terraform_${TERRAFORM_VERSION}_linux_amd64.zip
ENV TERRAFORM_URL=https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/${TERRAFORM_FILENAME}
ENV TERRAFORM_SHA256SUM=6b8ce67647a59b2a3f70199c304abca0ddec0e49fd060944c26f666298e23418

RUN apk add --update git bash wget

RUN wget -q ${TERRAFORM_URL} \
  && echo "${TERRAFORM_SHA256SUM}  ${TERRAFORM_FILENAME}" | sha256sum -c
RUN unzip ${TERRAFORM_FILENAME} -d /bin
RUN rm -f ${TERRAFORM_FILENAME}
