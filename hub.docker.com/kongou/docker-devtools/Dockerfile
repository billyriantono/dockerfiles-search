FROM ubuntu

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y vim gcc g++ git unzip make python python-dev python-setuptools libssl-dev python-pip ruby ruby-dev wget --no-install-recommends && \
    apt-get clean && rm -rf /var/cache/apt/archives/* /var/lib/apt/lists/*
RUN pip install wheel && \
    pip install ansible awscli aws-shell azure-cli azure-cli-shell pywinrm && \
    gem install serverspec test-kitchen kitchen-ec2 kitchen-ansiblepush kitchen-azurerm winrm winrm-fs --no-ri --no-rdoc && \
    wget https://releases.hashicorp.com/terraform/0.9.3/terraform_0.9.3_linux_amd64.zip && \
    unzip terraform_0.9.3_linux_amd64.zip && mv terraform /usr/bin/
