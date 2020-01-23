FROM dockersamples/visualizer

# Metadata
LABEL mantainer="Gius. Camerlingo <gcamerli@gmail.com>"
LABEL version="1.0"
LABEL description="Viewer for Docker Swarm."

# Docker image name
ENV NAME=swarm-view

# Timezone
ENV TZ="Europe/Paris"

# Group
RUN addgroup -S docker

# User
RUN adduser -S -g docker docker

# Home
ENV HOME=/home/docker

# Permissions
RUN chown -R docker:docker $HOME

# Change user
USER docker
