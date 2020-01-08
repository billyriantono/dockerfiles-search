# ansible

FROM alpine:latest
LABEL maintainer "Jonathan Roemer <dev@roemersoftworks.com>"

RUN apk update && apk upgrade && apk --no-cache add \
    ansible

# Set up a non-root user for the program
RUN addgroup -S appgroup && adduser -S appuser -G appgroup
WORKDIR /home/appuser
USER appuser

ENTRYPOINT [ "ansible" ]
