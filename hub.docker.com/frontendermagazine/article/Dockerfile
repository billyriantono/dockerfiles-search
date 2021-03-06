# docker run -it node:8.12-alpine /bin/bash
# ---- Base Node ----
FROM node:10-alpine AS base
# Preparing
RUN mkdir -p /var/app && chown -R node /var/app
# Set working directory
WORKDIR /var/app
# Copy project file
COPY package.json .
COPY package-lock.json .

#
# ---- Dependencies ----
FROM base AS dependencies
RUN apk add --update python build-base
# install node packages
RUN npm ci --only=prod --silent
# copy production node_modules aside
RUN cp -R node_modules prod_node_modules
# install ALL node_modules, including 'devDependencies'
RUN npm ci --silent
# Run in production mode

#
# ---- Test & Build ----
# run linters, setup and tests
FROM dependencies AS build
COPY . .
# Setup environment variables
RUN npm run build

#
# ---- Release ----
FROM base AS release
RUN apk add --update bash && rm -rf /var/cache/apk/*
# copy production node_modules
COPY --from=dependencies /var/app/prod_node_modules ./node_modules
COPY --from=build /var/app/build ./build
# COPY --from=build /var/app/source ./source

# Setup environment variables
ENV NODE_ENV=production
# expose port and define CMD
EXPOSE 4000
CMD npm run start
