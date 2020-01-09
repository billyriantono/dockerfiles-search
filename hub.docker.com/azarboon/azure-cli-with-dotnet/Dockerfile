FROM microsoft/dotnet:2.2-sdk

# installs dependencies
RUN apt-get update && apt-get install apt-transport-https lsb-release software-properties-common dirmngr -y 

# modify source list
RUN echo "deb [arch=amd64] https://packages.microsoft.com/repos/azure-cli/ stretch main" | tee /etc/apt/sources.list.d/azure-cli.list


# Get the Microsoft signing key

RUN apt-key --keyring /etc/apt/trusted.gpg.d/Microsoft.gpg adv --keyserver packages.microsoft.com --recv-keys BC528686B50D79E339D3721CEB3E94ADBE1229CF

# Install cli
RUN apt-get update && apt-get install azure-cli

# Install npm  and related dependencies
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash - \
&& apt install nodejs && npm i -g yarn 
