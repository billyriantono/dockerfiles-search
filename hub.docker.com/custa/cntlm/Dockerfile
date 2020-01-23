FROM ubuntu:16.04
RUN apt-get -y update && apt-get -y install cntlm && rm -rf /var/lib/apt/lists/*
ENTRYPOINT ["/usr/sbin/cntlm"]
CMD ["-f"]
