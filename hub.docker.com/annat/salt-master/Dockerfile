FROM debian:stretch
RUN apt-get update && apt-get install -y salt-master && rm -rf /var/lib/apt/lists/*
CMD ["/usr/bin/salt-master"]