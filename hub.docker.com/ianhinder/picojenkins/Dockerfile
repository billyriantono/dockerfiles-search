FROM jenkins/jenkins:lts

USER root

RUN apt-get update && apt-get install -y build-essential && rm -rf /var/lib/apt/lists/*
RUN apt-get update && apt-get install -y cmake gcovr check && rm -rf /var/lib/apt/lists/*

USER jenkins
