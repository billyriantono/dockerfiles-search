# How to build

#   docker build -t roblabs/mapbox-gl-build .

# How to spin up

#   cd mapbox-gl-native
#   # Run and preserve the docker container
#   docker run -it      -v $(pwd):/opt/mapbox-gl-native roblabs/mapbox-gl-build /bin/bash
#   # Run and remove the docker container
#   docker run -it --rm -v $(pwd):/opt/mapbox-gl-native roblabs/mapbox-gl-build /bin/bash


# https://hub.docker.com/r/runmymind/docker-android-sdk/
FROM runmymind/docker-android-sdk:ubuntu-standalone

# Good habit to run before installing
RUN apt-get update

# Install Build tools
RUN apt-get install -y \
  curl nodejs npm git build-essential zlib1g-dev automake \
  libtool xutils-dev make cmake pkg-config python-pip \
  libcurl4-openssl-dev libpng-dev libsqlite3-dev

# Install NDK
RUN /opt/android-sdk-linux/tools/bin/sdkmanager "ndk-bundle" || exit 1

# Externally accessible data is by default put in /data
WORKDIR /opt/mapbox-gl-native
#ADD . /opt/mapbox-gl-native
