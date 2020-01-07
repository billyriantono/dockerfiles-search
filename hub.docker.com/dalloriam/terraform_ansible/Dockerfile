FROM python:3.6

RUN apt-get update
RUN apt-get install unzip

RUN pip install ansible

RUN wget https://releases.hashicorp.com/terraform/0.11.3/terraform_0.11.3_linux_amd64.zip
RUN unzip terraform_0.11.3_linux_amd64.zip
RUN mv terraform /usr/local/bin

RUN  wget https://github.com/adammck/terraform-inventory/releases/download/v0.7-pre/terraform-inventory_v0.7-pre_linux_amd64.zip
RUN unzip terraform-inventory_v0.7-pre_linux_amd64.zip
RUN mv terraform-inventory /usr/local/bin
