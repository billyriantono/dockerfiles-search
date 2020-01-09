FROM ubuntu
RUN apt-get update && \
    apt-get install -yf git curl gnupg gnupg2 gnupg1 wget apt-transport-https software-properties-common && \
    wget -q https://packages.microsoft.com/config/ubuntu/18.04/packages-microsoft-prod.deb && dpkg -i packages-microsoft-prod.deb && rm -f packages-microsoft-prod.deb && \
    add-apt-repository universe && \
    apt-get update && \
    apt-get install -y dotnet-sdk-2.2 

