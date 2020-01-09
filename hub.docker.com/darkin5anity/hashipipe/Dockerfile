FROM alpine:latest

RUN apk add unzip wget git && \
	wget https://releases.hashicorp.com/packer/1.3.4/packer_1.3.4_linux_amd64.zip && \
	wget https://releases.hashicorp.com/terraform/0.11.11/terraform_0.11.11_linux_amd64.zip && \
	unzip terraform_0.11.11_linux_amd64.zip && \
	unzip packer_1.3.4_linux_amd64.zip && \
	mv terraform /usr/bin && \
	mv packer /usr/bin && \
	mkdir /home/git

WORKDIR	/home/git

CMD	terraform -version && packer -version



