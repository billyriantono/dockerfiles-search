FROM jenkins/jenkins:slim

# Switch to user root so we have permission to do stuff
USER root

# Install Docker command
WORKDIR /tmp

RUN curl https://download.docker.com/linux/static/stable/x86_64/docker-18.09.6.tgz --output docker.tgz \
    && echo "9af9440de24163de4b1bcb4ef459e7ed1ab2c8d9  docker.tgz" | sha1sum --check \
    && tar xvf docker.tgz \
    && cp ./docker/docker /usr/bin/ \
    && rm -rf ./docker \
    && rm docker.tgz

# Add user jenkins to the docker group
RUN groupadd -f docker && usermod -a -G docker jenkins

# Switch back to jenkins user
USER jenkins

