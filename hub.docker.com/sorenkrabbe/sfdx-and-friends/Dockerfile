FROM node:lts-alpine

# install misc utilities
RUN apk add --update --no-cache openssh ca-certificates openssl bash jq git

# install sfdx
RUN npm install sfdx-cli --global

# Set non root user
USER node
