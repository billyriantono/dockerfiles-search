FROM alpine:3.3
# Create app directory and bundle app source
RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app
COPY . /usr/src/app

# Install node.js and app dependencies
RUN echo '@edge http://nl.alpinelinux.org/alpine/edge/main' >> /etc/apk/repositories \
  && apk update && apk upgrade \
  && apk add --no-cache nodejs

# Expose port
EXPOSE 30000

CMD [ "node", "app.js" ]
