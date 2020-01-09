FROM alexldocker/jnlp-slave-alpine-aws
USER root
RUN wget -q https://releases.hashicorp.com/terraform/0.9.11/terraform_0.9.11_linux_amd64.zip && \
    unzip terraform_0.9.11_linux_amd64.zip -d /usr/local/bin/ && \
    mv /usr/local/bin/terraform /usr/local/bin/terraform_0.9.11 && \
    rm -f terraform_0.9.11_linux_amd64.zip

USER jenkins
