FROM alpine:3.7

RUN apk add --no-cache gcc musl-dev

COPY . /usr/src/myapp
WORKDIR /usr/src/myapp
ENTRYPOINT ["/usr/src/myapp/flow.sh"]
