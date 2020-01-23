FROM mcr.microsoft.com/dotnet/core/sdk:3.1
RUN apt-get update && apt-get install ca-certificates apt-transport-https -y
RUN apt-get install libc6-dev libgdiplus libx11-dev -y
RUN apt-key adv --fetch-keys https://dl.yarnpkg.com/debian/pubkey.gpg && echo "deb https://dl.yarnpkg.com/debian/ stable main" > /etc/apt/sources.list.d/yarn.list
RUN apt-key adv --fetch-keys https://deb.nodesource.com/gpgkey/nodesource.gpg.key && echo "deb https://deb.nodesource.com/node_11.x stretch main" > /etc/apt/sources.list.d/nodesource.list
RUN dotnet tool install --global coverlet.console
RUN apt-get update && apt-get install nodejs=11.15.0-1nodesource1 -y
RUN apt-get install yarn=1.17.3-1 -y
