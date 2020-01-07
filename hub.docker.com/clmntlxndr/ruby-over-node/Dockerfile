FROM node:12-alpine

# As of now, node is based on alpine 3.9
FROM ruby:2-alpine3.9

RUN apk add --no-cache libstdc++

ENV YARN_VERSION 1.19.1

COPY --from=0 /usr/local/share/doc/node /usr/local/share/doc/node
COPY --from=0 /usr/local/include/node /usr/local/include/node
COPY --from=0 /usr/local/bin/node /usr/local/bin/node
COPY --from=0 /usr/local/lib/node_modules /usr/local/lib/node_modules
COPY --from=0 /opt/yarn-v$YARN_VERSION /opt/yarn-v$YARN_VERSION

RUN ln -s ../lib/node_modules/npm/bin/npm-cli.js /usr/local/bin/npm
RUN ln -s ../lib/node_modules/npm/bin/npx-cli.js /usr/local/bin/npx
RUN ln -s /opt/yarn-v$YARN_VERSION/bin/yarn /usr/local/bin/yarn \
	  && ln -s /opt/yarn-v$YARN_VERSION/bin/yarnpkg /usr/local/bin/yarnpkg

RUN gem install bundler:2.0.2
