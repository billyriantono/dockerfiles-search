FROM python:2-alpine

WORKDIR /

RUN \
  apk --no-cache add \
    bash \
    build-base \
    gcc \
    git \
    libffi-dev \
    make \
    musl-dev \
    openssl-dev \
    openssh \
    zip \
    unzip \
    wget \
  && \
  pip install awscli --upgrade && \
  pip install boto boto3 ansible virtualenv && \
  wget --no-verbose https://releases.hashicorp.com/terraform/0.11.3/terraform_0.11.3_linux_amd64.zip && \
  unzip terraform_0.11.3_linux_amd64.zip && \
  mv terraform /usr/local/bin && \
  rm terraform_0.11.3_linux_amd64.zip

COPY init.sh /root/init.sh

RUN chmod a+x /root/init.sh

ENTRYPOINT ["/root/init.sh"]
