# Node Env - an environment built on the openjdk image that includes
# Node.js 4.5 and NPM 2.15.9
FROM openjdk
MAINTAINER Daniel Maple <danielm@ibcos.co.uk>

## Install node.js
# Download the node.js installer
RUN curl -o /tmp/node-setup https://deb.nodesource.com/setup_4.x && \
    # Grant execution permissions to the installer
    chmod +x /tmp/node-setup && \
    # Run the installer
    /tmp/node-setup && \
    # Install node.js and npm through the package manager
    apt-get install -y nodejs && \
    # Remove temporary file
    rm /tmp/node-setup
