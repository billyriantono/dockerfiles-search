FROM fedora:latest

MAINTAINER Alan Clucas

RUN dnf install -y ansible unzip openssh-clients && \
    dnf update -y && \
    dnf -y clean all

RUN curl https://releases.hashicorp.com/packer/1.4.4/packer_1.4.4_linux_amd64.zip > /tmp/packer.zip && \
    unzip -o /tmp/packer.zip -d /usr/local/bin && \
	rm /tmp/packer.zip
