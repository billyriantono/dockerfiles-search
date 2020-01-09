#
# Original idea from FPM Dockerfile
#
# https://github.com/dockerfile/fpm
#

# Pull base image.
FROM ruby

# Install FPM.
RUN gem install fpm && \
apt update && \
apt install -y rpm rpm-common && \
apt -y clean && \
apt -y autoclean

# Define working directory.
WORKDIR /data

# Define default command.
CMD ["bash"]
