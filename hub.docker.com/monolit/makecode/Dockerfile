##
## Base
##
FROM node:stretch AS base
RUN apt-get update -q -y && apt-get install -q -y \
    dumb-init
RUN useradd --user-group --create-home --shell /bin/false app
ENV HOME=/home/app
WORKDIR $HOME
ENTRYPOINT ["/usr/bin/dumb-init", "--"]

##
## Production dependencies
##
FROM base AS production-dependencies
COPY src/package.json ./
RUN chown app:app ./package.json
USER app
RUN npm set progress=false && \
    npm config set depth 0 && \
    npm install --only=production

##
## Build and test
##
FROM production-dependencies AS tested-build
USER root
RUN apt-get update -q -y && apt-get install -q -y \
    libgnome-keyring-dev \
    libusb-1.0-0-dev
RUN npm set progress=false && \
    npm config set depth 0 && \
    npm install
COPY src ./
RUN npm run build
RUN npm test

##
## Production
##
FROM production-dependencies AS production
COPY --from=2 $HOME/built/packaged ./built/packaged
USER root
RUN chown -R app:app ./built
USER app
EXPOSE 3000
CMD ["npm", "run", "serve"]
