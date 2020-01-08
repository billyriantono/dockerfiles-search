############################################################
# Dockerfile to run Memcached Containers
# Based on Debian Jessie
# Based on Digital Ocean Post
# https://www.digitalocean.com/community/articles/docker-explained-how-to-create-docker-containers-running-memcached
############################################################

FROM debian:jessie
MAINTAINER Kévin Gomez <contact@kevingomez.fr>

# Update the default application repository sources list
RUN apt-get update

# Install Memcached
RUN apt-get install -y memcached

# Port to expose (default: 11211)
EXPOSE 11211

# Default Memcached run command arguments
CMD ["-m", "128"]

# Set the user to run Memcached daemon
USER daemon

# Set the entrypoint to memcached binary
ENTRYPOINT memcached
