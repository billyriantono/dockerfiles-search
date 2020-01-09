FROM ubuntu:latest
RUN apt-get update
MAINTAINER Larry Cai "larry.caiyu@gmail.com"
RUN apt-get install -y curl make
RUN curl https://get.docker.io/builds/Linux/x86_64/docker-latest -o /usr/local/bin/docker
RUN chmod +x /usr/local/bin/docker
CMD ["bash"]
