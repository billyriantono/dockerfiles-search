FROM mcr.microsoft.com/dotnet/core/sdk:3.0 AS builder

# INSTALL PRE REQS
RUN apt-get update -yq \
    && apt-get install curl gnupg -yq \
    && curl -sL https://deb.nodesource.com/setup_10.x | bash \
    && apt-get install nodejs -yq \
    && apt-get install unzip -yq && \
    curl -sSL https://aka.ms/getvsdbgsh | /bin/sh /dev/stdin -v latest -l /vsdbg

# SET NPM CONTEXT
RUN npm -g config set user root