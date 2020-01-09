FROM nodered/node-red-docker

USER root

# User configuration directory volume
VOLUME ["/data"]

RUN npm install -g npm@5.7.1 \
    && npm config set bin-links false
    
# Configure Python environment
RUN apt-get update \
    && apt-get install -y python-pip \
    && pip install virtualenv

COPY startup /startup

USER node-red

RUN npm config set bin-links false

ENTRYPOINT ["/startup/startup.sh"]
