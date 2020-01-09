# Upgrade only-office/documentserver image to avoid postgres Issue

# Build:    docker build -t exo-documentserver .
#
# Run:      docker run -i -t -d exo-documentserver

FROM  onlyoffice/documentserver:5.2.7.2
LABEL maintainer="eXo Platform <docker@exoplatform.com>"

# Update and upgrade packages
RUN apt-get -qq update && \
  apt-get -qq -y upgrade && \
  rm -rf /var/lib/apt/lists/*

