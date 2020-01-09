FROM golang:1.6-onbuild

# Define rancher version
# ENV RANCHER_CLI_VERSION=v0.5.1

# Install dependencies and rancher
RUN apt-get install ca-certificates && \
	apt-get install curl
RUN	curl -sSL "http://static.novacloud.cz.s3-website.eu-central-1.amazonaws.com/rancher-cli/rancher_linux-amd64" > /usr/local/bin/rancher && \
	chmod +x /usr/local/bin/rancher && \
	rm -rf /var/cache/*

RUN make install

ENTRYPOINT []
