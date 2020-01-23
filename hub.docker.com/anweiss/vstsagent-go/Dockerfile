FROM ubuntu:14.04
MAINTAINER Andrew Weiss <andrew.weiss@outlook.com>

# Environment variables
ENV vsts_username ""
ENV vsts_password ""
ENV vsts_url ""
ENV vsts_agentname $HOSTNAME
ENV vsts_agentpool default
ENV vsts_service_username vsoservice
ENV vsts_service_password vsoservice
ENV LANG en_US.UTF-8

# Set locale
RUN locale-gen en_US.UTF-8

# Add repo source and update package listing
RUN sh -c 'echo "deb [arch=amd64] http://apt-mo.trafficmanager.net/repos/dotnet/ trusty main" > /etc/apt/sources.list.d/dotnetdev.list'
RUN apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
RUN apt-get update

# Install dependencies
RUN apt-get install -y libicu52 dotnet=1.0.0.001598-1 expect git curl g++ gcc libc6-dev make mercurial

#  Create a service user 
RUN echo "${vsts_service_username}\n${vsts_service_password}\n\n\n\n\n\n\n" | adduser ${vsts_service_username}

# Install Go

ENV GOLANG_VERSION 1.6.2
ENV GOLANG_DOWNLOAD_URL https://golang.org/dl/go$GOLANG_VERSION.linux-amd64.tar.gz
ENV GOLANG_DOWNLOAD_SHA256 e40c36ae71756198478624ed1bb4ce17597b3c19d243f3f0899bb5740d56212a

RUN curl -fsSL "$GOLANG_DOWNLOAD_URL" -o golang.tar.gz \
	&& echo "$GOLANG_DOWNLOAD_SHA256  golang.tar.gz" | sha256sum -c - \
	&& tar -C /usr/local -xzf golang.tar.gz \
	&& rm golang.tar.gz
RUN chmod -R 777 /usr/local/go

ENV GOPATH /opt/buildagent/go
ENV PATH $GOPATH/bin:/usr/local/go/bin:$PATH

RUN mkdir -p "$GOPATH/src" "$GOPATH/bin" && chmod -R 777 "$GOPATH"

RUN go get github.com/mitchellh/gox

# Create VSTS agent build directories
RUN mkdir /opt/buildagent/_work
WORKDIR /opt/buildagent

# Install VSTS agent
RUN curl -kSLO https://github.com/Microsoft/vsts-agent/releases/download/v2.99.0/vsts-agent-linux-2.99.0-0428.tar.gz
RUN tar zxvf vsts-agent-linux-2.99.0-0428.tar.gz

# Copy expect file
COPY ConfigureAgent.expect ConfigureAgent.expect


RUN su ${vsts_service_username}

# Configure CMD
WORKDIR /opt/buildagent
RUN chown -R ${vsts_service_username} /opt/buildagent
COPY runagent.sh runagent.sh
COPY go-wrapper /usr/local/bin/
RUN chmod +x runagent.sh
CMD ["/bin/sh","./runagent.sh"]