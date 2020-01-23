FROM node:alpine
LABEL maintainer="Francisca Gonzalez <fragongod@alum.us.es>"

RUN mkdir -p /opt/app

# set our node environment, either development or production
# defaults to production, compose overrides this to development on build and run
ARG NODE_ENV=production
ENV NODE_ENV $NODE_ENV

# default to port 80 for node
ARG PORT=80
ENV PORT $PORT
EXPOSE $PORT

WORKDIR /opt/app

COPY package*.json ./

RUN npm install && npm cache clean --force
COPY . /opt/app

CMD [ "npm","run", "start" ]