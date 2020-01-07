FROM mcr.microsoft.com/dotnet/core/sdk:2.2

# set up node
ENV NODE_VERSION 8.16.0
ENV NODE_DOWNLOAD_SHA b391450e0fead11f61f119ed26c713180cfe64b363cd945bac229130dfab64fa
RUN curl -SL "https://nodejs.org/dist/v${NODE_VERSION}/node-v${NODE_VERSION}-linux-x64.tar.gz" --output nodejs.tar.gz \
    && echo "$NODE_DOWNLOAD_SHA nodejs.tar.gz" | sha256sum -c - \
    && tar -xzf "nodejs.tar.gz" -C /usr/local --strip-components=1 \
    && rm nodejs.tar.gz \
    && ln -s /usr/local/bin/node /usr/local/bin/nodejs