
FROM microsoft/dotnet:2.1-sdk-stretch
LABEL maintainer="Peter Clemenko"

# Install system components
RUN apt-get update
RUN apt-get install -y curl gnupg apt-transport-https sudo

# Import the public repository GPG keys
RUN curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -

# Register the Microsoft Product feed
RUN sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-debian-stretch-prod stretch main" > /etc/apt/sources.list.d/microsoft.list'

# Update the list of products
RUN sudo apt-get update

RUN sudo apt-get install -y libicu-dev

# Install PowerShell
RUN sudo apt-get install -y powershell

#ENTRYPOINT ["/bin/bash"]
ENTRYPOINT ["pwsh"]

