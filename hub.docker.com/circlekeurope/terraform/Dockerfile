ARG ALPINE_VERSION

FROM alpine:${ALPINE_VERSION:-latest}
MAINTAINER Vegard Hansen (vegard.hansen@circlekeurope.com)

ARG VERSION
ENV VERSION=${VERSION}

RUN apk --update add ca-certificates wget unzip
ADD https://releases.hashicorp.com/terraform/${VERSION}/terraform_${VERSION}_linux_amd64.zip /
RUN unzip terraform_${VERSION}_linux_amd64.zip
RUN rm terraform_${VERSION}_linux_amd64.zip
RUN chmod +x terraform
RUN mv terraform /usr/bin/

CMD ["/bin/sh"]
