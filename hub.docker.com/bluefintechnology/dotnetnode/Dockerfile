FROM microsoft/dotnet:2.2-sdk

ENV NODE_VERSION 10.15.2
ENV NODE_DOWNLOAD_SHA 65e66599b275e2c41a882610a841a990e0570ed03bfccc378e031c475a3dae52
RUN curl -SL "https://nodejs.org/dist/v${NODE_VERSION}/node-v${NODE_VERSION}-linux-x64.tar.gz" --output nodejs.tar.gz \
    && echo "$NODE_DOWNLOAD_SHA nodejs.tar.gz" | sha256sum -c - \
    && tar -xzf "nodejs.tar.gz" -C /usr/local --strip-components=1 \
    && rm nodejs.tar.gz \
    && ln -s /usr/local/bin/node /usr/local/bin/nodejs \
    && apt-get update \
    && apt-get install bzip2 \
    && apt-get install libfontconfig --assume-yes
  
