FROM maven:3.5.3-jdk-8
LABEL maintainer="srouaix@ippon.fr"

ENV PATH="~/bin:${PATH}"

RUN mkdir -p ~/bin \
 && cd ~/bin \
 && apt-get update \
 && apt-get install -y unzip python-pip 

RUN cd ~/bin \
 && wget https://releases.hashicorp.com/terraform/0.11.7/terraform_0.11.7_linux_amd64.zip \
 && unzip terraform_0.11.7_linux_amd64.zip

RUN cd ~/bin \
 && pip install awscli
