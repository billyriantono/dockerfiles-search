FROM mesosphere/mesos-slave:0.28.0-2.0.16.ubuntu1404

RUN echo "deb http://apt.dockerproject.org/repo ubuntu-trusty main" \
         > /etc/apt/sources.list.d/docker.list
RUN gpg --keyserver hkp://keyserver.ubuntu.com:80 --recv F76221572C52609D && gpg --export --armor F76221572C52609D | apt-key add -
RUN apt-get update \
    && apt-get install -y docker-engine \
    && rm -rf /var/lib/apt/lists/*
