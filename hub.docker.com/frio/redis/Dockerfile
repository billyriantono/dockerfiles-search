FROM stackbrew/ubuntu:saucy

MAINTAINER dockerfile "http://dockerfile.github.io"
MAINTAINER frio "http://frio.name/"

# Install Redis.
RUN DEBIAN_FRONTEND=noninteractive apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y software-properties-common
RUN DEBIAN_FRONTEND=noninteractive add-apt-repository -y ppa:chris-lea/redis-server
RUN DEBIAN_FRONTEND=noninteractive apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y redis-server

# Expose ports.
EXPOSE 6379

# Define an entry point.
ENTRYPOINT ["redis-server"]
