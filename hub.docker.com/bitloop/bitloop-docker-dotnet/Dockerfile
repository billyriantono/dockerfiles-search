FROM microsoft/dotnet
MAINTAINER BitLoop <info@bitloop.eu>

# Global install yarn package manager
RUN apt-get update && apt-get install -y curl apt-transport-https && \
    curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
    echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && \
    apt-get update && apt-get install -y yarn

RUN apt-get install --yes curl
RUN curl --silent --location https://deb.nodesource.com/setup_6.x | bash -
RUN apt-get install --yes nodejs
RUN apt-get install --yes build-essential

# Angular CLI
RUN npm install -g @angular/cli yarn && npm cache clean


#PowerShell

# Install dependencies and clean up
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        apt-utils \
        ca-certificates \
        curl \
        apt-transport-https \
    && rm -rf /var/lib/apt/lists/*

RUN apt-get install curl apt-transport-https

# Import the public repository GPG keys
RUN curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -

# Register the Microsoft Product feed
RUN sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/debian/stretch/prod stretch main" > /etc/apt/sources.list.d/microsoft.list'

# Update the list of products
RUN apt-get update

# Install PowerShell
RUN apt-get install -y powershell

CMD ["/bin/bash"]
ENTRYPOINT []
        



