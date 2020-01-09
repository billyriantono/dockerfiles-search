FROM node:12.12.0-alpine

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

# Path to local installs
ENV PATH /usr/src/app/node_modules/.bin:$PATH
# Path to global installs
ENV PATH /usr/local/node_modules/.bin:$PATH

ENV NODE_ENV development

RUN npm install -g nodemon
COPY ./package*.json ./
RUN npm install -g

COPY ./ ./

CMD ["npm", "start"]