from node:8-alpine

RUN apk --no-cache --update-cache add \
    openssl \
    bash \
    jq \
    git \
    zip

# Install serverless

RUN npm install -g serverless

CMD [ "node" ]