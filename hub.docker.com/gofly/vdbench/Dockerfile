FROM openjdk:8-jre
RUN apt-get update && \
    apt-get install -y --no-install-recommends csh && \
    rm -rf /var/lib/apt/lists/*
RUN curl -L http://7xlwfg.com1.z0.glb.clouddn.com/vdbench503.zip -o vdbench503.zip && \
    mkdir vdbench && cd vdbench && \
    unzip ../vdbench503.zip && rm ../vdbench503.zip && \
    mkdir -p /opt && mv ../vdbench /opt
WORKDIR /opt/vdbench
ENTRYPOINT ["/opt/vdbench/vdbench"]
