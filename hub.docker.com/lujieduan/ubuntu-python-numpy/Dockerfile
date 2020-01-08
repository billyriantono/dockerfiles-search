FROM ubuntu:18.04

RUN apt-get update \
    && apt-get install -y python3 python3-pip gettext-base \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

RUN pip3 install numpy
CMD ["/bin/bash"]
