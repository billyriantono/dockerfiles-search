# base image
FROM mcr.microsoft.com/dotnet/core/sdk:3.1

# Install ZIP:
RUN apt-get update
RUN apt-get install -y zip

# Install Azure CLI
# Docs https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-apt?view=azure-cli-latest

RUN	curl -sL https://aka.ms/InstallAzureCLIDeb | bash
