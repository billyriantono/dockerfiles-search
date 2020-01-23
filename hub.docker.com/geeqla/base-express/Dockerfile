FROM node:8
ENV NODE_ENV=production
WORKDIR /usr/src/base-express
COPY . .
RUN yarn install
EXPOSE 3000
CMD yarn start