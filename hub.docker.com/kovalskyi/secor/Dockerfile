FROM maven:3.5.3-jdk-8
LABEL maintainer="Mykhailo Kovalskyi"

# Clone and checkout 0.26-SNAPSHOT
WORKDIR /tmp
RUN git clone https://github.com/pinterest/secor.git
RUN cd secor && git checkout 8d24ce54ed224acc6d53127d5f31207d74596504

# Assemble package
WORKDIR /tmp/secor
RUN rm -f src/main/config/secor*
RUN mvn package -Dmaven.test.skip=true

# Extract package and cleanup
RUN mkdir -p /srv
RUN tar -zxvf target/secor-0.26-SNAPSHOT-bin.tar.gz -C /srv
WORKDIR /srv
RUN rm -rf /tmp/*

