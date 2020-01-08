# Ubuntu based PHP container

# General documentation links:
# - https://docs.docker.com/get-started/part2/#introduction
# - https://docs.docker.com/develop/develop-images/dockerfile_best-practices/
# - https://blog.ubuntu.com/2018/07/09/minimal-ubuntu-released

# After installing docker you may need to:
#  sudo usermod -a -G docker $USER
# After that system restart is required.

FROM ubuntu:18.04
COPY ./install.sh /
RUN /install.sh > /dev/null
CMD ["/bin/bash"]