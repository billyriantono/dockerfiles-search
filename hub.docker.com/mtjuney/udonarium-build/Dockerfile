FROM node:lts-slim

ENV UDONARIUM_VERSION "v1.8.2"

WORKDIR /udonarium

# install Angular CLI
RUN npm install -g @angular/cli

# install dependences packages
RUN curl "https://raw.githubusercontent.com/TK11235/udonarium/${UDONARIUM_VERSION}/package.json" > package.json
RUN curl "https://raw.githubusercontent.com/TK11235/udonarium/${UDONARIUM_VERSION}/package-lock.json" > package-lock.json
RUN npm install
