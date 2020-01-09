FROM node:9.0.0
RUN npm i pm2 -g
RUN curl -o- -L https://yarnpkg.com/install.sh | bash
RUN rm -rf /tmp/node_modules
COPY package.json /tmp/package.json
COPY yarn.lock /tmp/yarn.lock
RUN cd /tmp && yarn
RUN mkdir -p /opt/app/api && cp -a /tmp/node_modules /opt/app/api
COPY . /opt/app/api
WORKDIR /opt/app/api