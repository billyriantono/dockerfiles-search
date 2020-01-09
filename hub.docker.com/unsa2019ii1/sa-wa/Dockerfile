FROM node:12.7.0-alpine

RUN npm install -g serve

COPY ./src/dist/ ./dist

CMD ["serve", "-s", "dist"]
