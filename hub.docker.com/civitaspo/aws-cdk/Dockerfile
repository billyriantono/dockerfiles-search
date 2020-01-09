FROM node:10-alpine as nd
RUN  npm install -g aws-cdk@0.15.2

FROM maven:3-jdk-8-alpine
COPY --from=nd /usr/local/bin/node /usr/local/bin/node
COPY --from=nd /usr/local/lib/node_modules /usr/local/lib/node_modules
COPY --from=nd /opt/yarn-v1.10.1 /opt/yarn-v1.10.1
COPY --from=nd /usr/local/include/node /usr/local/include/node
RUN  cd /usr/local/bin                                         \
         && ln -nfs ../lib/node_modules/aws-cdk/bin/cdk cdk    \
         && ln -nfs ../lib/node_modules/npm/bin/npm-cli.js npm \
         && ln -nfs ../lib/node_modules/npm/bin/npx-cli.js npx \
         && ln -nfs /opt/yarn-v1.10.1/bin/yarn yarn            \
         && ln -nfs /opt/yarn-v1.10.1/bin/yarnpkg yarnpkg

ENTRYPOINT ["cdk"]
