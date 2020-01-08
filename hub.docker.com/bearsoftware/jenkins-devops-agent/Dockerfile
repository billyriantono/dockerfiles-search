FROM jenkins/jnlp-slave

#Add Docker, Ansible, Terraform

USER root

RUN apt-get update

RUN apt-get install -y \
  git python python-pip bash curl gcc
  
#RUN apt-get install -y --reinstall systemd 

#Need to install docker command line this way - apt-get docker installs only the gui one
RUN curl -sSL https://get.docker.com/ | sh

RUN usermod -aG docker jenkins

#RUN systemctl enable docker.service

RUN pip install --upgrade pip
RUN pip install awscli boto3 ansible

RUN curl https://releases.hashicorp.com/terraform/0.11.11/terraform_0.11.11_linux_amd64.zip -o terraform_0.11.11_linux_amd64.zip && \
  unzip terraform_0.11.11_linux_amd64.zip && \
  mkdir -p /usr/local/sbin && \
  mv terraform /usr/local/sbin && \
  rm -f terraform_0.11.11_linux_amd64.zip
