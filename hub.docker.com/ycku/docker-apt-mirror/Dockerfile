FROM debian:buster-slim

RUN apt update
RUN apt install -y --no-install-recommends apt-mirror

ADD mirror.list /etc/apt/mirror.list
RUN mkdir -p /mirrors
RUN apt-mirror

CMD ["/bin/bash"]
