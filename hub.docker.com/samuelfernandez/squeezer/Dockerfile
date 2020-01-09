### Build stage ###
FROM node:10.16.0 as builder

LABEL authors="Samuel Fernandez"

# Configure environment
ENV TERM xterm
ENV npm_config_loglevel error

# Install lerna globally
RUN npm install lerna --global

# Set WORKDIR and install dependencies
WORKDIR /usr/src/squeezer
COPY package.json package-lock.json ./
RUN npm ci

# Copy packages
COPY packages/travis-github ./packages/travis-github

# Run Lerna
COPY lerna.json .
RUN lerna bootstrap --ci --ignore-scripts --force-local --hoist

# Copy source files
COPY . .

# Set node in production mode
ENV NODE_ENV=production

# Build
RUN lerna run lint
RUN lerna run test:ci
RUN lerna run build

# Run as a non-root user
USER node