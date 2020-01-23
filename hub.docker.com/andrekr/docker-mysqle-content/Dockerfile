FROM node:10.9-alpine

RUN apk add --update --no-cache make git

RUN npm install -g dockerfilelint

ENTRYPOINT ["dockerfilelint"]

