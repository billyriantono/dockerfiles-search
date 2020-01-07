FROM node:10-stretch

COPY ./package.json /package.json
RUN ["npm", "install", "pnpm", "-g"]
RUN ["pnpm", "install"]
