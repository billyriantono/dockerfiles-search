FROM node:alpine

# Change global package directory (allowing packages to be installed globally without root user)
ENV NPM_CONFIG_PREFIX=~/.npm-global

RUN su node -c 'npm install -g @angular/cli@latest'

COPY --chown=node:node rootfs/home/node /home/node

USER node:node
ENTRYPOINT ["/bin/sh", "-l"]
