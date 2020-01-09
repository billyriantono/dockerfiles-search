FROM nereus/gs-openjdk10:latest

SHELL ["/bin/bash","-c"] 

RUN apt-get update; \
    apt-get install -y git; \
    apt-get clean;

WORKDIR /root/build

CMD ["bash"]