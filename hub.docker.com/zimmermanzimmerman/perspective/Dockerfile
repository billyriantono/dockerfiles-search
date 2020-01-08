FROM node:6.12

RUN npm -g install yarn

RUN mkdir -p /app/src
WORKDIR /app/src
ENV PATH /app/src/node_modules/.bin:${PATH}

ADD package.json /app/src
ADD yarn.lock /app/src
RUN yarn install

ADD . /app/src

# files not needed for Docker (values configured through env vars)
# but creating dummies for not breaking transip setups
RUN cp /app/src/server/config/urls.sample.js /app/src/server/config/urls.js
RUN cp /app/src/client/app/config.sample.js /app/src/client/app/config.js

RUN npm run build

CMD ["/app/src/bin/docker-cmd.sh"]
