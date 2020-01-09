# base image
FROM alpine:3.7

ARG VERSION
ENV PORT=3000 NODE_ENV=production
RUN apk add --update nodejs nodejs-npm

# set working directory
RUN mkdir -p /app
WORKDIR /app


COPY . .

COPY package*.json ./
ADD package.json /app/package.json
COPY webpack.config.js /app/webpack.config.js
COPY .eslintrc /app/.eslintrc
RUN npm install
VOLUME ["/app/logs"]
EXPOSE 3000

CMD ["npm", "start"]
