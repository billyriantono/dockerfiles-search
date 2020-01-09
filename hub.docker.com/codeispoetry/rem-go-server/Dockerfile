
FROM node:10-alpine
WORKDIR /app
COPY package.json yarn.lock ./
RUN yarn install --pure-lockfile && yarn cache clean --production
COPY . .
EXPOSE 4000
CMD ["npm", "start"]
