FROM ubuntu:14.10
MAINTAINER Marcell Spies

# Install latest version of mono-complete and cleanup, when finished
RUN \
  apt-key adv --keyserver pgp.mit.edu --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF \
  && echo "deb http://download.mono-project.com/repo/debian wheezy main" > /etc/apt/sources.list.d/mono-xamarin.list \
  && apt-get -q update \
  && apt-get -qy install mono-complete \
  && rm -rf /var/lib/apt/lists/*

# Define working directory.
WORKDIR /data

# Volumes
VOLUME ["/data"]

# Define default command.
CMD ["bash"]