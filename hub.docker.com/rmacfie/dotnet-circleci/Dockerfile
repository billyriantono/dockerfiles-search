FROM microsoft/dotnet:2.1-sdk

# - - - - - - - - - - - -
# Install Docker CLI
# - - - - - - - - - - - -
ENV DOCKER_VERSION 17.03.2-ce
RUN curl -SL "https://download.docker.com/linux/static/stable/x86_64/docker-$DOCKER_VERSION.tgz" -o /tmp/docker.tgz \
    && tar -xzf /tmp/docker.tgz -C /tmp \
    && mv /tmp/docker/* /usr/bin \
    && rm /tmp/docker.tgz

# - - - - - - - - - - - -
# Install NodeJS
# - - - - - - - - - - - -
ENV NODE_VERSION 8.11.2
RUN curl -SL "https://nodejs.org/dist/v${NODE_VERSION}/node-v${NODE_VERSION}-linux-x64.tar.gz" -o /tmp/nodejs.tgz \
    && tar -xzf /tmp/nodejs.tgz -C /usr/local --strip-components=1 \
    && rm /tmp/nodejs.tgz \
    && ln -s /usr/local/bin/node /usr/local/bin/nodejs

# - - - - - - - - - - - -
# Install yarn
# - - - - - - - - - - - -
RUN npm install --global yarn
