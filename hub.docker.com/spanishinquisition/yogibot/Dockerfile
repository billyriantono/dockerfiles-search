FROM node:12.6

WORKDIR /usr/app
COPY package-lock.json package.json ./
RUN npm install --no-progress --ignore-optional

WORKDIR /usr/app/src
COPY src/ ./

CMD ["node", "."]