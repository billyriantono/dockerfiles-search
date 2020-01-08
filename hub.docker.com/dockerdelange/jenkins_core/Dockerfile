FROM jenkins
 # Switch to root to install .NET Core SDK
USER root

# Just for my sanity... Show me this distro information!
RUN uname -a && cat /etc/*release

#This to install docker client START
#ARG DOCKER_CLIENT=docker-17.06.2-ce.tgz
#RUN cd /tmp/ 
#RUN curl -sSL -O https://download.docker.com/linux/static/stable/x86_64/${DOCKER_CLIENT}
#RUN tar zxf ${DOCKER_CLIENT} &&\
#	mkdir -p /usr/local/bin &&\
#	mv ./docker/docker /usr/local/bin &&\
#	chmod +x /usr/local/bin/docker &&\
#	rm -rf /tmp/*
#Finish docker client

# Based on instructiions at https://docs.microsoft.com/en-us/dotnet/core/linux-prerequisites?tabs=netcore2x
# Install depency for dotnet core 2.
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    curl libunwind8 gettext apt-transport-https && \
    curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg && \
    mv microsoft.gpg /etc/apt/trusted.gpg.d/microsoft.gpg && \
    sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-debian-stretch-prod stretch main" > /etc/apt/sources.list.d/dotnetdev.list' && \
    apt-get update

# Install the .Net Core framework, set the path, and show the version of core installed.
#RUN apt-get install apt-transport-https && \
#RUN	apt-get update
RUN	apt-get install -y dotnet-sdk-2.1.104
RUN export PATH=$PATH:$HOME/dotnet
RUN dotnet --version

# Good idea to switch back to the jenkins user.
USER jenkins