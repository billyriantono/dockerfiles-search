FROM mcr.microsoft.com/dotnet/core/sdk:2.2

ENV SOLIDITY_VERSION 0.5.2
ENV SOLIDITY_DOWNLOAD_URL https://github.com/ethereum/solidity/releases/download/v$SOLIDITY_VERSION/solc-static-linux

RUN curl -SL $SOLIDITY_DOWNLOAD_URL --output /usr/bin/solc && chmod +x /usr/bin/solc
