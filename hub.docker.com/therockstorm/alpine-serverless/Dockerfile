FROM mhart/alpine-node:8

RUN apk update && \
apk upgrade && \
apk add --no-cache --update bash py-pip ca-certificates && \
update-ca-certificates && \
rm -rf /var/cache/apk/* && \
pip install --upgrade pip && \
pip install --no-cache-dir awscli && \
npm install -g npm && \
npm install -g serverless --ignore-scripts && \
npm cache clean --force
