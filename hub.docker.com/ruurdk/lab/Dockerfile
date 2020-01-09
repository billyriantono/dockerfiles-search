FROM bosh/cli2

RUN apt-get install -y git curl dnsutils wget unzip

RUN wget https://releases.hashicorp.com/terraform/0.11.7/terraform_0.11.7_linux_amd64.zip && \
unzip terraform_0.11.7_linux_amd64.zip && \
rm terraform_0.11.7_linux_amd64.zip && \
mv terraform /usr/local/bin
