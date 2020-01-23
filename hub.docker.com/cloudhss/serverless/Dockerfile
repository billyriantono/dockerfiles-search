FROM node:8.10

COPY ./apiGateway.js /tmp/
COPY ./removeAlias.js /tmp/

RUN npm install -g serverless@1.38.0 && \
    npm install -g serverless-aws-alias@1.7.1 && \
    cp -f /tmp/apiGateway.js /usr/local/lib/node_modules/serverless-aws-alias/lib/stackops/ && \
    cp -f /tmp/removeAlias.js /usr/local/lib/node_modules/serverless-aws-alias/lib/
