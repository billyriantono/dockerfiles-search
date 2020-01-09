FROM undancer/ubuntu:18.04

LABEL author="undancer, undancer@gmail.com"

RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get -y install software-properties-common && \
    add-apt-repository ppa:webupd8team/java && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*
RUN apt-get update && \
    echo "oracle-java8-installer shared/accepted-oracle-license-v1-1 select true" | debconf-set-selections && \
    echo "oracle-java8-unlimited-jce-policy shared/accepted-oracle-license-v1-1 select true" | debconf-set-selections && \
    DEBIAN_FRONTEND=noninteractive \
    apt-get -y install \
      oracle-java8-installer \
      oracle-java8-unlimited-jce-policy \
      oracle-java8-set-default \
    && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

CMD ["/usr/bin/java -version"]
# CMD ["bash"]
