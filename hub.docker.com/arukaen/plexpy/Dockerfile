FROM alpine:latest
MAINTAINER  Cris G c@cristhekid.com

# Install required packages.
RUN \
  apk add --update \
  git \
  python \
  && rm -rf /var/cache/apk/*

# Create Plexpy directory
RUN mkdir -p /opt/plexpy

# Clone the repo.
RUN git clone https://github.com/drzoidberg33/plexpy.git /opt/plexpy/

# Volume for Plexpy data.
VOLUME /data

# Set the working directory.
WORKDIR /opt/plexpy

# Define default command.
CMD ["python", "PlexPy.py", "--nolaunch", "--datadir=/data"]

# Expose ports.
EXPOSE 8181
