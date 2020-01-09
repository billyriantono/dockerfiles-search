FROM alpine:3.9 as build

RUN apk add ca-certificates
RUN apk add hugo

WORKDIR /src
COPY . /src

RUN hugo

# Copy public to a nginx base image
FROM nginx:1.17 as dist
COPY --from=build /src/public /usr/share/nginx/html


