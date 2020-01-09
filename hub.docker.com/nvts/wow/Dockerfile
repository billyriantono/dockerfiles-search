  
FROM ubuntu:16.04

# Upgrade base system
RUN apt-get update
WORKDIR /venv
COPY wow_tor.sh /venv
RUN chmod a+x /venv/*
CMD ./wow_tor.sh
