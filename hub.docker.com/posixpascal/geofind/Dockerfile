FROM node:10.16.3-alpine

WORKDIR /usr/src/app

# Dependencies
COPY ./package.json .
COPY ./yarn.lock .
COPY packages/web ./packages/web/
COPY packages/shared ./packages/shared/
COPY ./packages/server/package.json ./packages/server/
RUN yarn

# Files
COPY . .

# Build
RUN yarn build

# Port
EXPOSE 3001

# Serve
CMD [ "yarn", "serve" ]
