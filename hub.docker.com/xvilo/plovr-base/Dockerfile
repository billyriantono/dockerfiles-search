# Builds the image xvilo/plovr-base
FROM openjdk:8

# Install deps
RUN apt update && apt install -y \
  git \
  ant \
  gcc \
  python \
  python-dev

# Build BUCK
RUN git clone https://github.com/facebook/buck.git /buck/
WORKDIR /buck
RUN ant
RUN ln -sf /buck/bin/buck /usr/bin/
