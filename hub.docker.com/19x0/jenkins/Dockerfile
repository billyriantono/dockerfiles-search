FROM jenkins/jenkins:lts
USER root
RUN apt-get update \
    && apt-get upgrade -y \
    && apt-get install -y --no-install-recommends python-pip python-setuptools python-wheel \
    && pip --no-cache-dir install simiki \
    && rm -rf /var/lib/apt/lists/*
#volume /var/jenkins_home
# drop back to the regular jenkins user - good practice
USER jenkins