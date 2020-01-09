FROM alpine:latest

# update and install dependencies
RUN apk --no-cache --update upgrade && apk --no-cache add ca-certificates curl

WORKDIR /

# copy compiled portainer build
COPY /dist /

# remove original templates.json and replace with custom templates.json
RUN rm /templates.json

# RUN curl https://gitlab.com/appealtoheavenllc/portainer-templates/raw/master/node-templates.json > /templates.json
COPY /src/node-templates.json /templates.json

VOLUME /data
WORKDIR /
EXPOSE 9000

ENTRYPOINT ["/portainer"]