# Build frontend
FROM node as build-frontend
WORKDIR /src
COPY frontend/package.json frontend/yarn.lock ./
RUN yarn
COPY frontend/ ./
RUN yarn build

# Build backend
FROM golang:latest AS build-backend
WORKDIR /src
COPY ./backend/ ./
RUN GOPATH=/ GOOS=linux GOARM=7 GOARCH=arm go build -ldflags="-w -s" main.go

# Create image
FROM scratch
WORKDIR /app
COPY --from=build-backend /src/main ./
COPY --from=build-backend /src/config.conf ./
COPY --from=build-frontend /src/build/ ./build/
COPY --from=build-backend /usr/local/go/lib/time/zoneinfo.zip /
ENV ZONEINFO=/zoneinfo.zip
ENTRYPOINT ["./main"]
