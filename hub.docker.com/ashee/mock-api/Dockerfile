#
# mock-api: a minimal restful api in nodejs
#
# build:
#   docker build --force-rm -t ashee/mock-api .
# run:
#   docker run --rm -it --name mock-api -p 3000:3000 ashee/mock-api
# push:
#   docker push ashee/mock-api
#

### BASE
FROM node:8.9.4-alpine AS base
LABEL maintainer "Amitava Shee <amitava.shee@gmail.com>"

# Set the working directory
WORKDIR /app

# Copy project specification and dependencies lock files
COPY package.json yarn.lock ./

# Install yarn
RUN apk --no-cache add yarn

### DEPENDENCIES
FROM base AS dependencies

RUN yarn --production
RUN cp -R node_modules /tmp/node_modules
RUN yarn

### RELEASE
FROM base AS release
COPY --from=dependencies /tmp/node_modules ./node_modules
COPY . .
EXPOSE 3000

CMD yarn run start
