FROM node:10.15.3-stretch-slim

RUN npm install -g tiddlywiki

# Setup wiki volume
VOLUME /var/lib/tiddlywiki
WORKDIR /var/lib/tiddlywiki

# Add run script
ADD run-wiki /usr/local/bin/run-wiki

# Meta
CMD ["/usr/local/bin/run-wiki"]
EXPOSE 8080

