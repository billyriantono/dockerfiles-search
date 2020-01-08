# Start from this base layer
FROM alpine:3.7

LABEL maintainer="tylerhaigh1994@me.com"

# Add a new layer with this software installed
RUN apk add --update nodejs nodejs-npm

COPY . /hello-docker-express

WORKDIR /hello-docker-express
RUN npm install

EXPOSE 8080

ENTRYPOINT [ "node", "./app.js" ]