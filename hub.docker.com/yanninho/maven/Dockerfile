FROM java:8u40-jdk

RUN apt-get update && \
    apt-get -y upgrade && \
    apt-get install -y maven

VOLUME ["/workspace"]
WORKDIR /workspace
