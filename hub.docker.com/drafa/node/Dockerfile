FROM buildpack-deps:wheezy

MAINTAINER Rafael Tarazón <*******@****.***>

# Global environment variables.
ENV ROOT_DIR="/node"
ENV SERVER_DIR="$ROOT_DIR/server"
ENV \
  APP_DIR="$SERVER_DIR/app" \
  RESOURCES_DIR="$ROOT_DIR/resources" \
  APP="app.js" \
  DEFAULT_PORT="8888" \
  NODE_VERSION="4.1.1" \
  NPM_CONFIG_LOGLEVEL="info" \
  PATH="$PATH:/usr/local/bin" \
  NODE_PATH="$NODE_PATH:/usr/local/lib/node_modules"

# Info about this image
LABEL \
  about.origin="This image was inspired by https://github.com/nodejs/docker-node/blob/3136e8429bd4017cf55a09761faf866c2cb8b104/4.1/wheezy/Dockerfile"  \
  author.name="Rafael Tarazón" \
  author.email="******@****.***" \
  author.website="****.com" \
  image.created="2015/09/27" \
  image.description="This image creates a Node container"  \
  image.updated="2015/10/08" \
  image.version="1." \
  env.node.version="$NODE_VERSION" \
  env.path="$PATH" \
  env.node.path="$NODE_PATH" \
  env.npm.log_level="$NPM_CONFIG_LOGLEVEL" \
  env.default_port="$DEFAULT_PORT" \
  repository.issues="https://github.com/drafa/node/issues" \
  repository.github="https://github.com/drafa/node"

# Create tree
RUN \
  mkdir -p $APP_DIR \
  && mkdir $RESOURCES_DIR

VOLUME $SERVER_DIR

# Our app dir
WORKDIR $SERVER_DIR

# Copy contents on our container
COPY ./resources/ $RESOURCES_DIR
COPY ./tmp/ /tmp/

# Execute all commands for generate a container
RUN \
  /tmp/keys.sh \
  && /tmp/install-node.sh \
  && sleep 1 \
  && rm -rf /tmp/*

EXPOSE $DEFAULT_PORT

CMD $RESOURCES_DIR/run.sh
