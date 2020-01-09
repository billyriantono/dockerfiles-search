# build go

FROM golang:alpine as builder
COPY ./ /src
RUN apk add --no-cache git && cd /src && go build -o goapp

# build angular

FROM node:12-alpine as ngbuilder
WORKDIR /src
COPY ./webApp/package*.json ./webApp/yarn.lock ./
RUN yarn add --force node-sass && yarn install
COPY ./webApp/ ./
RUN npm run buildProd

# final stage

FROM alpine:latest
WORKDIR /app
COPY --from=builder /src/goapp /app/
COPY --from=ngbuilder /src/dist/ /app/public/

ENV GIN_MODE=release
ENV TREADSHARE_API_URL=http://127.0.0.1:8080/v1

EXPOSE 3000
ENTRYPOINT ./goapp
