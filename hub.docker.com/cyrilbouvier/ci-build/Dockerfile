#  docker build -t cyrilbouvier/ci-build .
FROM debian:stretch

RUN apt-get update && \
    apt-get install -y cmake make build-essential git wget curl gcc g++ \
                       python2.7 python3 perl libgmp-dev gnuplot xsltproc && \
  # Removing documentation packages *after* installing them is kind of hacky,
  # but it only adds some overhead while building the image.
  apt-get --purge remove -y .\*-doc$ && \
  # Remove more unnecessary stuff
  apt-get clean -y && rm -rf /var/lib/apt/lists/*
