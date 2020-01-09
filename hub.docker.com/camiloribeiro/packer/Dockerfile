FROM centos

RUN curl -o packer_0.9.0.zip https://releases.hashicorp.com/packer/0.9.0/packer_0.9.0_linux_amd64.zip
RUN yum update -y && yum install zip unzip -y
RUN unzip packer_0.9.0.zip -d /usr/local/

WORKDIR /app

ENTRYPOINT ["/usr/local/packer"]
