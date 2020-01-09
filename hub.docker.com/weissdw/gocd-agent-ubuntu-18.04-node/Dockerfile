######### Base image
FROM gocd/gocd-agent-ubuntu-18.04:v19.9.0

######### Setup build environment
USER root

# curl
RUN apt-get update && apt-get -y install curl

# Node
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash -
RUN apt-get update && apt-get install -y nodejs

# yarn
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" > /etc/apt/sources.list.d/yarn.list
RUN apt-get update && apt-get install -y yarn