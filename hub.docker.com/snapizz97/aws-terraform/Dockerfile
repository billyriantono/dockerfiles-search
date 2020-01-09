FROM hashicorp/terraform

RUN apk --no-cache add \ 
      zip \
      bash \
      curl \
      less \
      groff \
      jq \
      git \
      python \
      py-pip \
      py2-pip && \
      pip install --upgrade pip awscli s3cmd && \
      mkdir /root/.aws

ENTRYPOINT []