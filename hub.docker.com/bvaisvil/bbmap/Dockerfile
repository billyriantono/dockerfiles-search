FROM ubuntu:latest
RUN apt-get update && apt-get install curl tar gzip default-jdk -y  
RUN curl -L https://sourceforge.net/projects/bbmap/files/BBMap_38.49.tar.gz/download | tar xvz
ENTRYPOINT ["/bbmap/bbmap.sh"]
