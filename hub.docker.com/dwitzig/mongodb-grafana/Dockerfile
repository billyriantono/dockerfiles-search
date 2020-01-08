FROM node:10-alpine

ENV NODE_ENV=production
ENV PORT=80

RUN mkdir -p /usr/src/app

WORKDIR /usr/src/app

COPY . .
RUN rm -rf ./git 

RUN npm install
WORKDIR /usr/src/app

EXPOSE 80

CMD ["npm", "run", "server"]
