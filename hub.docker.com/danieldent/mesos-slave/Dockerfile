FROM mesosphere/mesos-slave:0.26.0-0.2.145.ubuntu1404
ADD https://apt.dockerproject.org/gpg /tmp/docker.gpg.key
RUN echo "c836dc13577c6f7c133ad1db1a2ee5f41ad742d11e4ac860d8e658b2b39e6ac1 /tmp/docker.gpg.key" | sha256sum -c \
   && apt-key add /tmp/docker.gpg.key \
   && echo "deb http://apt.dockerproject.org/repo ubuntu-trusty main" > /etc/apt/sources.list.d/docker.list \
   && DEBIAN_FRONTEND=noninteractive apt-get update -q \
   && DEBIAN_FRONTEND=noninteractive apt-get dist-upgrade -y \
   && DEBIAN_FRONTEND=noninteractive apt-get install -y docker-engine=1.9.1-0~trusty \
   && rm -Rf /var/lib/apt /var/cache/apt
