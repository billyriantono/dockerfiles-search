from ubuntu:16.04

RUN apt-get update && apt-get install -y cpuburn && rm -rf /var/lib/apt/lists/*
COPY runBurn.sh /
CMD /runBurn.sh
