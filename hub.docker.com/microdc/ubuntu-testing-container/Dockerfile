FROM ubuntu
ENV LC_ALL C.UTF-8
RUN apt-get update && \
    apt-get install -y shellcheck \
                       python3 \
                       python3-pip \
                       yamllint
RUN pip3 install --upgrade pip \
                           pyyaml
