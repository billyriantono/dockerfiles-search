FROM microsoft/dotnet:2.1.403-sdk 
 
# Install Docker
RUN set -ex \
	&& apt-get update \
	&& apt-get install -y apt-transport-https ca-certificates curl software-properties-common --no-install-recommends \
	&& curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add - \
	&& add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable" \
	&& apt-get update \
	&& apt-cache policy docker-ce \
	&& apt-get install -y docker-ce --no-install-recommends \
	&& docker --version \
	&& rm -rf /var/lib/apt/lists/*
	
# Install Build Requirements
RUN set -ex \
	&& apt-get update \
	&& curl -sL https://deb.nodesource.com/setup_8.x | bash - \
	&& apt-get install -y nodejs python-dev build-essential libcurl3 --no-install-recommends \
	&& nodejs --version \
	&& npm --version \
	&& rm -rf /var/lib/apt/lists/*