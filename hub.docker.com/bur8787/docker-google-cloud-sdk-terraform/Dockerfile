FROM google/cloud-sdk

WORKDIR /work
RUN apt-get install unzip
RUN curl -sL https://releases.hashicorp.com/terraform/0.11.7/terraform_0.11.7_linux_amd64.zip > terraform.zip
RUN unzip terraform.zip
RUN mv terraform /usr/local/bin/
RUN rm -rf terraform.zip
