FROM golang:1.10-alpine

# Set timezone
ENV TZ=Europe/Madrid
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# Install req packages
RUN apk --update add curl git && rm /var/cache/apk/*