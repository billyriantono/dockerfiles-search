FROM alpine/socat as prod

EXPOSE 1234
ENV SRC_URL="localhost:80"

ENTRYPOINT socat tcp-listen:1234,fork,reuseaddr tcp-connect:${SRC_URL}

