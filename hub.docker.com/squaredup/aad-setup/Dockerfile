FROM ubuntu:18.04

RUN apt-get update -qq && \
	apt-get install -qqy --no-install-recommends unzip wget curl apt-transport-https lsb-release gpg ca-certificates

RUN curl -sL --insecure https://packages.microsoft.com/keys/microsoft.asc | \
    gpg --dearmor | \
    tee /etc/apt/trusted.gpg.d/microsoft.asc.gpg > /dev/null

RUN echo "deb [trusted=yes arch=amd64] https://packages.microsoft.com/repos/azure-cli/ $(lsb_release -cs) main" | \
    tee /etc/apt/sources.list.d/azure-cli.list

RUN apt-get update && \
	apt-get install azure-cli

RUN wget https://releases.hashicorp.com/terraform/0.11.13/terraform_0.11.13_linux_amd64.zip && \
	unzip terraform_0.11.13_linux_amd64.zip && \
	chmod +x /terraform 

ADD squaredup.tf /squaredup.tf
RUN	./terraform init

CMD az login --use-device-code && \
	./terraform apply