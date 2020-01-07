FROM jenkins/jenkins:lts

USER root
RUN apt-get update \
    && apt-get install -y \
        ansible \
        sshpass \
    && apt-get autoremove \
    && rm -rf /var/lib/apt/lists/*
USER jenkins