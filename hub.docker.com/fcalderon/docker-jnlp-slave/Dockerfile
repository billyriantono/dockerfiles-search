# Docker Jenkins JNPL slave

FROM jenkinsci/jnlp-slave

USER root

# update the repository sources list
# and install dependencies

RUN apt-get update -qq && apt-get install -qqy \
    apt-transport-https \
    ca-certificates \
    curl \
    lxc \
    iptables

RUN curl -sSL https://get.docker.com/ | sh

USER jenkins
