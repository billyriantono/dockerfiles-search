FROM gocd/gocd-agent-ubuntu-16.04:v18.6.0

RUN apt-get update \
 && apt-get upgrade -y \
 && apt-get install build-essential libssl-dev openjdk-8-jdk maven -y \
 && apt-get install firefox unixodbc-dev -y \
 && curl -sL "https://deb.nodesource.com/setup_8.x" | bash - \
 && apt-get install nodejs -y \
 && groupadd --gid 1001 node \
 && useradd --uid 1001 --gid node --shell /bin/bash --create-home node

RUN apt-get install software-properties-common -y \
 && add-apt-repository ppa:jonathonf/python-3.6 -y \
 && apt-get update \
 && apt-get install python3.6 python3.6-dev python3-setuptools python3-testresources python3-pip -y

# workaround for issue https://github.com/angular/angular-cli/issues/7389
USER node
RUN mkdir /home/node/.npm-global
ENV PATH=/home/node/.npm-global/bin:$PATH
ENV NPM_CONFIG_PREFIX=/home/node/.npm-global
RUN npm i -g @angular/cli@1.5.4 \
 && npm i -g swagger@0.7.5 \
 && npm i -g mocha@5.0.1 \
 && npm i -g mocha-junit-reporter@1.17.0 \
 && npm i -g sonarqube-scanner@2.0.2

USER root
