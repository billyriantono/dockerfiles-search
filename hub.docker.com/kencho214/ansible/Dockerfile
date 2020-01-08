FROM ubuntu:18.04

RUN apt update && \
  apt install python3.7 -y && \
  apt install -y software-properties-common && \
  apt install -y curl && \
  add-apt-repository ppa:ansible/ansible && \
  apt update && \
  apt install -y ansible

CMD ["/bin/bash"]
