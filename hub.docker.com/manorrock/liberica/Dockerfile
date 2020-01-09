FROM manorrock/debian
ENV JAVA_VERSION 13.0.1
ENV JAVA_HOME /usr/local/jdk$JAVA_VERSION
ENV PATH $PATH:$JAVA_HOME/bin
RUN apt-get update && \
    apt-get -y install tar wget && \
    mkdir -p /usr/local && \
    cd /usr/local && \
    wget https://download.bell-sw.com/java/${JAVA_VERSION}/bellsoft-jdk${JAVA_VERSION}-linux-amd64.tar.gz && \
    tar xfvz bellsoft-jdk$JAVA_VERSION-linux-amd64.tar.gz && \
    rm bellsoft-jdk$JAVA_VERSION-linux-amd64.tar.gz && \
    mv jdk-${JAVA_VERSION} jdk${JAVA_VERSION} && \
    rm -rf /var/lib/apt/lists/*
WORKDIR /mnt
CMD ["bash"]

