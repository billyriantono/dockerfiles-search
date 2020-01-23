FROM node:alpine
LABEL maintainer "@flemay"

# update system and install packages
RUN apk --no-cache update && apk --no-cache upgrade \
    && apk --no-cache add --upgrade ca-certificates make zip curl

# install serverless
RUN npm install -g serverless

CMD ["serverless", "--version"]