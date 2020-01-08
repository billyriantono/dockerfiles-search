FROM jenkins/jenkins:lts

USER root

# Install docker client. See
# https://stackoverflow.com/questions/38675925/is-it-possible-to-install-only-the-docker-cli-and-not-the-daemon
# Enables the use of docker in Jenkins jobs.
# See
# https://jpetazzo.github.io/2015/09/03/do-not-use-docker-in-docker-for-ci/

ENV DOCKERVERSION=18.09.8
RUN curl -fsSLO https://download.docker.com/linux/static/stable/x86_64/docker-${DOCKERVERSION}.tgz \
  && tar xzvf docker-${DOCKERVERSION}.tgz --strip 1 \
                 -C /usr/local/bin docker/docker \
  && rm docker-${DOCKERVERSION}.tgz

USER jenkins
