FROM microsoft/dotnet:2.1.5-aspnetcore-runtime
 
# Install Node and supporting Python package
RUN set -ex \
	&& apt-get update \
	&& apt-get install -y curl wget gnupg --no-install-recommends \
	&& curl -sL https://deb.nodesource.com/setup_8.x | bash - \
	&& apt-get install -y nodejs --no-install-recommends \
	&& nodejs --version \
	&& npm --version \
	&& rm -rf /var/lib/apt/lists/*