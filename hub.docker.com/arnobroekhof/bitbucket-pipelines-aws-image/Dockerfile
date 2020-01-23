FROM maven:3-amazoncorretto-8

ARG TF_VERSION=0.11.13
ARG TF_DOWNLOAD_URL=https://releases.hashicorp.com/terraform/${TF_VERSION}/terraform_${TF_VERSION}_linux_amd64.zip


RUN yum install -y python3 pip3 unzip
RUN pip3 install -U setuptools \
    && pip3 install awscli \
    && curl -fsSL -o /tmp/terraform.zip ${TF_DOWNLOAD_URL} \
    && unzip /tmp/terraform.zip -d /usr/bin/ \
    && rm -rf /tmp/* \
    &&  yum clean all \
    &&  rm -rf /var/cache/yum \
    && rm -rf ~/.cache/pip