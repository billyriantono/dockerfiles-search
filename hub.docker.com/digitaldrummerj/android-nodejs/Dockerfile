FROM digitaldrummerj/android

MAINTAINER Justin James <digitaldrummerj@gmail.com>

ENV NODEJS_VERSION=5.11.1 \
    PATH=$PATH:/opt/node/bin

# NODEJS  
WORKDIR "/opt/node"

RUN apt-get install -y curl ca-certificates --no-install-recommends && \
    curl -sL https://nodejs.org/dist/v${NODEJS_VERSION}/node-v${NODEJS_VERSION}-linux-x64.tar.gz | tar xz --strip-components=1


# Clean up
RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
    apt-get autoremove -y && \
    apt-get clean 
