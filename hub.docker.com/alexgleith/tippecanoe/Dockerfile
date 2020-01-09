# Start from ubuntu
FROM ubuntu:16.04

# Install dependencies
RUN apt-get update && apt-get -y install \
	build-essential libsqlite3-dev zlib1g-dev wget unzip \
	protobuf-compiler libprotobuf-dev

ENV TC_VERSION 1.27.6

# Create a directory and copy in all files
WORKDIR /tmp
RUN wget https://codeload.github.com/mapbox/tippecanoe/zip/${TC_VERSION} -O /tmp/tippecanoe.zip \
	&& unzip /tmp/tippecanoe.zip

WORKDIR /tmp/tippecanoe-${TC_VERSION}

# Build tippecanoe
RUN make \
  && make install

# Remove the temp directory and unneeded packages
WORKDIR /
RUN rm -rf /tmp/tippecanoe-src \
  && apt-get -y remove --purge build-essential && apt-get -y autoremove

# Run the default command to show usage
CMD tippecanoe --help
