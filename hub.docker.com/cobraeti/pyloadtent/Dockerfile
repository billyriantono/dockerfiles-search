FROM python:3.7.4-buster
RUN mkdir /opt/terraform
RUN cd /tmp ; curl -O https://releases.hashicorp.com/terraform/0.12.8/terraform_0.12.8_linux_amd64.zip
RUN cd /tmp ; unzip terraform_0.12.8_linux_amd64.zip
RUN cd /tmp ; mv terraform /usr/bin/
