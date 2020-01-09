FROM ubuntu:14.04
MAINTAINER chauhan.suryaveer@gmail.com

RUN apt-get update -y && apt-get install -y gcc
RUN echo "HELLO"

EXPOSE 15000
# Simple startup script to avoid some issues observed with container restart 
ADD samplecserver.c /samplecserver.c
#COPY run.sh /run.sh
#RUN chmod +x run.sh
RUN gcc -o samplecserver samplecserver.c
ENTRYPOINT ["./samplecserver"]
