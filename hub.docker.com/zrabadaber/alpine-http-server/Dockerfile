from alpine:latest
run apk add --no-cache nodejs && apk add --no-cache git
run npm i -g http-server
workdir /home
add ./public /home
cmd ["http-server"]
expose 8080
