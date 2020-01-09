FROM techio/node-npm-runner
MAINTAINER Leonard Allain-Launay<leonard@codingame.com>
RUN ["npm", "install", "-g", "@angular/cli"]

RUN sh -c 'apt-get update'
RUN sh -c 'apt-get install -y apt-transport-https'

RUN sh -c 'curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -'
RUN sh -c 'echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list'

RUN sh -c 'apt-get update && apt-get install yarn -y'

COPY build.sh /project/build
