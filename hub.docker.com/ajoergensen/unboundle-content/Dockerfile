FROM alpine

RUN apk add --no-cache gcc musl-dev
COPY docker-machine-id-setup.c /tmp/
RUN cc /tmp/docker-machine-id-setup.c --static -o /tmp/docker-machine-id-setup
