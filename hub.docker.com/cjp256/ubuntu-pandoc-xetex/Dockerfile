# Pull base image.
FROM ubuntu:16.04
MAINTAINER Chris Patterson <cjp256@gmail.com>
RUN apt-get update && \
    apt-get install -y make texlive-xetex pandoc && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Default command
CMD ["bash"]
