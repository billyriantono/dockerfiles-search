FROM microsoft/vsts-agent:latest

RUN apt-get update \
 && apt-get install -y --no-install-recommends \
    mono-complete \
	unzip
	
RUN curl -sL https://github.com/GitTools/GitVersion/releases/download/v3.6.5/GitVersion_3.6.5.zip -o gitversion.zip \
 && unzip gitversion.zip -d /usr/local/gitversion
