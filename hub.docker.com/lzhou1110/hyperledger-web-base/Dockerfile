FROM node:6-alpine

# Create app directory
WORKDIR /usr/src/app
COPY . .

# RUN apk --help
# install node-gyp dependancies (for alpine only)
RUN apk add --update python make alpine-sdk libc6-compat

# Refer to package.json
RUN npm install && npm cache rm

# remove node-gyp dependancies (for alpine only)
# libc6-compat is essential for grps, so don't remove it
RUN apk del --purge python make alpine-sdk

