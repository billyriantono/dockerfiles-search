FROM ubuntu:16.04

# Install Mikero Tools dependencies
RUN apt-get update && apt-get upgrade -y && apt-get install -y liblzo2-2 libvorbis0a libvorbisfile3 libvorbisenc2 libogg0 curl
RUN apt-get clean && apt-get purge

# Install Mikero Tools to system
COPY bin/ /usr/local/bin
COPY lib/ /usr/local/lib

RUN curl https://mikero.bytex.digital/api/download?filename=depbo-tools-0.7.25-linux-64bit.tgz | tar --overwrite -xzC / --strip 1

# Update libraries
RUN ldconfig

# Run makepbo help if no other command specified
CMD makepbo -h
