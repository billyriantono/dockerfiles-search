FROM microsoft/dotnet:2.0.5-sdk-2.1.4-jessie

RUN apt-get update && apt-get install -y -q --no-install-recommends

# Set environment variables for NVM to use
ENV NVM_DIR /usr/local/nvm
ENV NODE_VERSION 6.5.0

# Install NVM
RUN curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.0/install.sh | bash \
    && . $NVM_DIR/nvm.sh \
    && nvm install $NODE_VERSION \
    && nvm alias default $NODE_VERSION \
    && nvm use default

# Add binaries to the path so commands are available
ENV NODE_PATH $NVM_DIR/v$NODE_VERSION/lib/node_modules
ENV PATH $NVM_DIR/versions/node/v$NODE_VERSION/bin:$PATH

# Confirm installation success
RUN node -v
RUN npm -v