FROM debian:jessie

# Install ssh & rsync
RUN apt-get update -qq \
    && apt-get install -y -qq \
    ssh \
    rsync \
    && rm -rf /var/lib/apt/lists/* \
    && apt-get autoremove

RUN mkdir /root/.ssh
# Seeting no strict host checking removes the question to ask about adding this host on each connection
RUN echo "StrictHostKeyChecking no" > /root/.ssh/config
CMD []
