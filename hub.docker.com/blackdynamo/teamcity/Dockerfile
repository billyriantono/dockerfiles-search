FROM sjoerdmulder/teamcity

# Prep node
RUN curl -sL https://deb.nodesource.com/setup_6.x | bash -

# Prep docker
RUN apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
RUN echo "deb https://apt.dockerproject.org/repo debian-jessie main" | tee /etc/apt/sources.list.d/docker.list

RUN apt-get update
RUN apt-get install -y nodejs build-essential docker-engine