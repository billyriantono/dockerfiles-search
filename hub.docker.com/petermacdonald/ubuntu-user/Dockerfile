FROM ubuntu:bionic

RUN apt-get update && \
    apt-get install -y sudo && \
    adduser user && \
    usermod -aG sudo user && \
    echo "user ALL=(root) NOPASSWD:ALL" > /etc/sudoers.d/user
RUN apt-get update && \
    apt-get install -y curl

CMD ["su", "-", "user", "-c", "/bin/bash"]