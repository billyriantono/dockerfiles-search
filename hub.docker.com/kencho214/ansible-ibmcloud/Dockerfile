FROM ubuntu:18.04

RUN apt update && \
  apt install python3.7 -y && \
  apt install -y software-properties-common && \
  apt install -y curl && \
  add-apt-repository ppa:ansible/ansible && \
  apt update && \
  apt install -y ansible

# Install IBM Cloud CLI
RUN curl -fsSL https://clis.cloud.ibm.com/install/linux | sh

# Install IBM Cloud CLI Plugins
RUN ibmcloud plugin install cloud-object-storage && \
  ibmcloud plugin install container-registry && \
  ibmcloud plugin install container-service

CMD ["/bin/bash"]
