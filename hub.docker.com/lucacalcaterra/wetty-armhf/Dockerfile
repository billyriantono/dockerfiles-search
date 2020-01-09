FROM node:8.15.0-stretch as builder

RUN apt-get update && \
        apt-get upgrade -y && \
        apt-get install build-essential -y && \
        apt-get install python -y

WORKDIR /usr/src/app
COPY . /usr/src/app
RUN yarn && \
    yarn build && \
    yarn install --production --ignore-scripts --prefer-offline

FROM node:8.15.0-stretch
LABEL maintainer="calcaterra.luca@gmail.com"
WORKDIR /usr/src/app
ENV NODE_ENV=production
RUN apt-get update && \
        apt-get upgrade -y && \
        apt-get install -y openssh-client && \
        apt-get install  sshpass -y

EXPOSE 3000
COPY --from=builder /usr/src/app/dist /usr/src/app/dist
COPY --from=builder /usr/src/app/node_modules /usr/src/app/node_modules
COPY package.json /usr/src/app
COPY index.js /usr/src/app
RUN mkdir ~/.ssh
RUN ssh-keyscan -H wetty-ssh >> ~/.ssh/known_hosts

ENTRYPOINT [ "node", "." ]
