FROM node:4-slim

ADD docker-provision.sh /tmp/
RUN cd /tmp/ && sh docker-provision.sh

WORKDIR /var/app

# run GitBook when the container starts
CMD ["gitbook", "serve"]
