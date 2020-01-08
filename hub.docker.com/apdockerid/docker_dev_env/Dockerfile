FROM apdockerid/visual_studio_code:release
LABEL maintainer="Andreas Pettersson"
# Change to root USER because inherited image is ended with code_user
USER root
ARG USER=code_user
ARG GROUP=code_group
ARG DOCKER_GROUP_ID=999
RUN groupadd -g ${DOCKER_GROUP_ID} docker
RUN usermod -aG docker ${USER}

# Install Docker and python tools
RUN apt-get update && apt-get install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common \
 && rm -rf /var/lib/apt/lists/*

RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -

RUN add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"

RUN apt-get update && apt-get install -y \
    docker-ce docker-ce-cli containerd.io \
 && rm -rf /var/lib/apt/lists/*

# Install tools
RUN pip3 install pylint
RUN pip3 install pep8
RUN pip3 install --upgrade autopep8

# Copy scripts
ARG DOCKER_DEV_SCRIPTS=/home/docker_dev_env/scripts
RUN mkdir -p ${DOCKER_DEV_SCRIPTS}
COPY /scripts/start_visual_studio_code.py ${DOCKER_DEV_SCRIPTS}
COPY /scripts/__init__.py ${DOCKER_DEV_SCRIPTS}
RUN chmod +x ${DOCKER_DEV_SCRIPTS}/start_visual_studio_code.py
RUN chown -R ${USER}:${GROUP} ${DOCKER_DEV_SCRIPTS}

USER ${USER}:${GROUP}
WORKDIR ${DOCKER_DEV_SCRIPTS}
