# ---------------------------------------------------------- #
#                         Dockerfile                         #
# ---------------------------------------------------------- #
# image:    java-node                                        #
# name:     wussama/java-node                                #
# repo:     https://github.com/oussamaABID/java-node         #
# ---------------------------------------------------------- #

FROM ubuntu:18.04
# Install helper
RUN apt-get update && apt upgrade && apt-get install -y wget git curl zip monit openssh-server git iptables ca-certificates daemon net-tools libfontconfig-dev

# Install Java
RUN echo "# Installing Java"
RUN apt-get install -y default-jre

RUN java --version

# Install NodeJS 
RUN echo "# Installing Nodejs" && \
    curl -sL https://deb.nodesource.com/setup_10.x | bash - && \
    apt-get install nodejs build-essential -y && \
    npm set strict-ssl false && \
    npm install -g npm@6.9.0 && \
    npm --version && \
    node --version


# Create Jenkins user.
RUN groupadd -g 10000 jenkins
RUN useradd jenkins --uid 1000 --create-home --home /home/jenkins/ --gid jenkins --shell /bin/bash

#Adding jenkins to sudoers list and making an alias for sudo docker
RUN echo "jenkins ALL=NOPASSWD: ALL" >> /etc/sudoers \
      && printf '#!/bin/bash\nsudo /usr/bin/docker "$@"' > /usr/local/bin/docker \
      && chmod +x /usr/local/bin/docker

USER jenkins
