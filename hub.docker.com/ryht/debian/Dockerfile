FROM debian:jessie
#ADD sources.list /etc/apt/
RUN apt-get update && \
    apt-get upgrade -y
RUN apt-get install -y nano \
                       wget && \
    apt-get clean
CMD ["/bin/bash"]
