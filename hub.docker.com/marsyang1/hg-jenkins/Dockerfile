# a naive Jenkins image
FROM jenkins
USER root
RUN apt-get update && \
    apt-get install -y mercurial meld && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*
USER jenkins
