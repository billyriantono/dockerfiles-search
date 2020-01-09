FROM sot001/python-base:latest

ENV TERRAFORM_VERSION=0.11.11

RUN apk add --update-cache ansible \
  && pip3.6 install awscli boto boto3 \
  && rm -rf /var/cache/apk/* \
  && wget -O /tmp/terraform_${TERRAFORM_VERSION}_linux_amd64.zip https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/terraform_${TERRAFORM_VERSION}_linux_amd64.zip \
  && unzip -d /usr/local/bin/ /tmp/terraform_${TERRAFORM_VERSION}_linux_amd64.zip

ENV ANSIBLE_GATHERING smart
ENV ANSIBLE_HOST_KEY_CHECKING false
ENV ANSIBLE_RETRY_FILES_ENABLED false
ENV ANSIBLE_ROLES_PATH /ansible/playbooks/roles
ENV ANSIBLE_SSH_PIPELINING True
ENV PYTHONPATH /ansible/lib
ENV PATH /ansible/bin:$PATH
ENV ANSIBLE_LIBRARY /ansible/library
 
WORKDIR /projects

CMD ["/bin/bash"] 
