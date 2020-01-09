FROM ubuntu:18.04

# ...put your own build instructions here...
LABEL maintainer="Mark Broughton <mark.broughton@travisperkins.co.uk"

ENV AWS_DEFAULT_REGION=eu-west-1
ENV ANSIBLE_VERSION=2.2.2
ENV TERRAFORM_VERSION=0.11.11

ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update -y 
RUN apt-get upgrade -y 
RUN apt-get -y install software-properties-common --fix-missing
RUN apt-get -y install openjdk-8-jdk   --fix-missing
RUN add-apt-repository -y ppa:deadsnakes/ppa 
RUN add-apt-repository universe
RUN apt-get update -y 
RUN apt-get upgrade -y 
RUN apt-get install -y apt-utils 
RUN apt-get install -y ca-certificates wget apt-transport-https vim nano tzdata git curl  
RUN apt-get install -y python3
RUN apt-get install -y python3-pip 
RUN apt-get install -y virtualenv  
RUN apt-get install -y ca-certificates 
RUN apt-get install -y unzip
RUN apt-get install -y gpg gnupg2 pass


RUN pip3 install --compile           ansible==${ANSIBLE_VERSION} awscli awslogs boto3 envtpl  \
 && pip3 install --upgrade --compile ansible==${ANSIBLE_VERSION} awscli awslogs boto3 envtpl 

 RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -                                  \
 && add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" \
 && apt-get update --quiet && DEBIAN_FRONTEND=noninteractive apt-get install --quiet --yes docker-ce

RUN wget -q -O - https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/terraform_${TERRAFORM_VERSION}_linux_amd64.zip                             | gunzip -c > /usr/local/bin/terraform        && chmod 755 -v /usr/local/bin/terraform        
RUN mkdir ~/.docker
RUN echo "{\"credsStore\":\"ecr-login\"}" > ~/.docker/config.json

RUN nohup dockerd &
