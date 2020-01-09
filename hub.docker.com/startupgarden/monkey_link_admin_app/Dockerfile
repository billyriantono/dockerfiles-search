FROM node:10.15.3

ENV NODE_ENV production
ENV NPM_CONFIG_PRODUCTION false
ENV PROJECT_ROOT /usr/src/app/

WORKDIR $PROJECT_ROOT

ARG API_URL
ARG CLIENT_URL

ENV API_URL    $API_URL
ENV CLIENT_URL $CLIENT_URL

COPY package.json package.json
COPY package-lock.json package-lock.json

RUN npm install

COPY . .

RUN npm run build

CMD ["npm", "start"]
