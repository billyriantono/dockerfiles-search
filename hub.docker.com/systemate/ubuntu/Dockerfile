#
# Ubuntu Dockerfile
#
# https://github.com/systemate/ubuntu
#

# Pull base image.
FROM dockerfile/ubuntu

# Install.
RUN \
  apt-get update && \
  apt-get install -y tzdata && \
  echo "Europe/Moscow" > /etc/timezone && \
  dpkg-reconfigure -f noninteractive tzdata

# Set environment variables.
ENV HOME /root

# Define working directory.
WORKDIR /root

# Define default command.
CMD ["bash"]
