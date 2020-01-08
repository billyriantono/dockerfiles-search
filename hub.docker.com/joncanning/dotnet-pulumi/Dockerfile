FROM mcr.microsoft.com/dotnet/core/sdk:3.0-disco
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash -
RUN wget -q https://packages.microsoft.com/config/ubuntu/19.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
RUN dpkg -i packages-microsoft-prod.deb
RUN apt-get update && apt-get install apt-transport-https dotnet-sdk-2.2 nodejs zip -y
RUN curl -fsSL https://get.pulumi.com | bash -
ENV PATH=$PATH:$HOME/.pulumi/bin
RUN $HOME/.pulumi/bin/pulumi version
