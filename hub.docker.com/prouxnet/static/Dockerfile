FROM node:8-alpine
MAINTAINER proux UG <info@proux.net>
ENV APP_HOME /app
COPY . /app
WORKDIR /app
RUN npm install --production
CMD ["npm","start"]
