# The instructions for the first stage
FROM node:lts-alpine as builder

ARG NODE_ENV=production
ENV NODE_ENV=${NODE_ENV}

RUN apk --no-cache add python make g++ git
RUN git config --global url.https://github.com/.insteadOf git://github.com/

COPY package*.json ./
RUN npm install

# The instructions for second stage
FROM node:lts-alpine

WORKDIR /opt/tatum/middleware
COPY --from=builder node_modules node_modules

COPY . .

EXPOSE 6543

CMD [ "npm", "start" ]
