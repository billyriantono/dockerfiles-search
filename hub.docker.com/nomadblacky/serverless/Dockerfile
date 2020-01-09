FROM node:10.15.3-alpine

RUN npm config set unsafe-perm true
RUN npm install -g serverless@1.39.1

ENTRYPOINT ["serverless"]
