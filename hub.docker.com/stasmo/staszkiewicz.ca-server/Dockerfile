FROM node:8

WORKDIR /home/node
USER node
COPY --chown=node package.json yarn.lock ./
RUN yarn install
COPY --chown=node . .

