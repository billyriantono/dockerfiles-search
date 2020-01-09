FROM debian:9.5-slim
# FROM microsoft/azure-cli:2.0.53
LABEL "com.github.actions.name"="issue-action"
LABEL "com.github.actions.description"="Write arguments to the standard output"
LABEL "com.github.actions.icon"="mic"
LABEL "com.github.actions.color"="purple"

LABEL "repository"=""
LABEL "homepage"=""
LABEL "maintainer"="haitam"
# simple docker file
# assumes located in the same folder as the application itself

# start with node 5 base image
FROM node:8

# run as non-root user inside the docker container
# see https://vimeo.com/171803492 at 17:20 mark
# RUN groupadd -r nodejs && useradd -m -r -g nodejs nodejs
# # now run as new user nodejs from group nodejs
# USER nodejs

# # Create an app directory (in the Docker container)
# RUN mkdir -p /usr/src/demo-server
# WORKDIR /usr/src/demo-server

# # Copy .npm settings and package.json into container
# COPY package.json /usr/src/demo-server
# COPY .npmrc /usr/src/demo-server
# # and install dependencies
# RUN npm install

# # Copy our source into container
# COPY src /usr/src/demo-server/src
# COPY server.js /usr/src/demo-server

# # If our server uses 1337 by default
# # expose it from Docker container
# EXPOSE 1337

# # Finally start the container command
# CMD ["node", "server.js"]

ADD entrypoint.sh /entrypoint.sh
COPY action-app /action-app 
ENTRYPOINT ["/entrypoint.sh"]
RUN cd /action-app && npm install