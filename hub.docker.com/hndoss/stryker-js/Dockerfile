FROM node:11-alpine 

WORKDIR /srv

RUN npm i -g \
  jest@24.5.0 \
  babel-jest \
  @stryker-mutator/core \
  @stryker-mutator/html-reporter \
  @stryker-mutator/javascript-mutator \
  @stryker-mutator/jest-runner \
  @stryker-mutator/typescript && \
  apk add git

ENTRYPOINT ["/usr/local/bin/stryker"]
