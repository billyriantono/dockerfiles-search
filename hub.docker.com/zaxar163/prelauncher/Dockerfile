FROM bellsoft/liberica-openjdk-debian:11
RUN apt-get update && apt-get install -y gcc g++ lib32z1
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
WORKDIR /root/
CMD ["bash"]
