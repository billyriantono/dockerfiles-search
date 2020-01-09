FROM ubuntu:16.04
# Maintainer will be deprecates soon (1.13)
MAINTAINER Joost van der Griendt <joost.van.der.griendt@nl.abnamro.com>
LABEL authors="Andre van der Zee <andre.van.der.zee@nl.abnamro.com>, Joost van der Griendt <joost.van.der.griendt@nl.abnamro.com>"
LABEL version="1.0.0"
LABEL description="Simple build container example for a dummy OCA"

RUN apt-get update && apt-get install -y nodejs-legacy npm git-all maven openjdk-8-jdk && rm -rf /var/lib/apt/lists/*
RUN npm install --global gulp@3.9.0
