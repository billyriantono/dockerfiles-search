FROM    ubuntu:14.04
RUN     apt-get update && apt-get install -y npm nodejs
RUN     ln -s `which nodejs` /usr/local/bin/node

# Clean up
RUN     apt-get clean && rm -rf /tmp/* /var/tmp/*
