FROM andremmfaria/linux-dind-build-image:latest
LABEL MAINTAINER="Andre Faria<andremarcalfaria@gmail.com>"

# Update system and install requirements
RUN apk update && \
    apk add --no-cache nodejs nodejs-npm

# Install gulp from npm
RUN npm config set unsafe-perm true && \
    npm install -g @angular/cli
