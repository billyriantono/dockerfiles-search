FROM mcr.microsoft.com/dotnet/core/sdk:2.2.105

LABEL version="2.2.105"
LABEL maintainer="Solidatus"

# Install dependencies
RUN apt-get update && \
    apt-get install -y curl apt-transport-https ca-certificates gnupg2 software-properties-common

# Install yarn
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash - && \
    curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
    echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && \
    apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y nodejs yarn && \
    yarn global add gulp-cli

# Install docker
RUN curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add - && \
    add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable" && \
    apt-get update && \
    apt-get install -y docker-ce

# Clean all files
RUN apt-get clean all
