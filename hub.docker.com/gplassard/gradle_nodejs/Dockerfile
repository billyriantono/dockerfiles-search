FROM gradle:jdk8

USER root
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash -
RUN apt-get update && apt-get install -y nodejs build-essential && rm -rf /var/lib/apt/lists/*
USER gradle

