FROM nikolausdemmel/ubuntu-dev-base:14.04

# non-persistent environment variables
ARG DEBIAN_FRONTEND=noninteractive

# Install libs
RUN apt-get update && apt-get install -y \
    libopencv-dev