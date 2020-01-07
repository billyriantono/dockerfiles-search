FROM gocd/gocd-agent-ubuntu-16.04:v18.1.0

RUN apt-get update \
 && apt-get upgrade -y \
 && apt-get install build-essential libssl-dev -y \
 && curl -sL "https://deb.nodesource.com/setup_8.x" | bash - \
 && apt-get install nodejs -y \
 && groupadd --gid 1001 node \
 && useradd --uid 1001 --gid node --shell /bin/bash --create-home node

# workaround for issue https://github.com/angular/angular-cli/issues/7389
USER node
RUN mkdir /home/node/.npm-global
ENV PATH=/home/node/.npm-global/bin:$PATH
ENV NPM_CONFIG_PREFIX=/home/node/.npm-global
RUN npm i -g @angular/cli@1.5.4 \
 && npm i -g swagger@0.7.5

USER root
