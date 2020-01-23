FROM microsoft/vsts-agent:latest

# Change current directory in docker image
WORKDIR /

# Backup vsts and restore at runtime
RUN mv /vsts /backup && rm -rf /vsts

# Create symbolic link to /tmp/vsts because tmp can be sole writable in heroku container
RUN mkdir -p /tmp/vsts && ln -nsf /tmp/vsts /vsts

# Patch start.sh
RUN sed -i 's/chown -R root:root/#chown -R root:root/g' /backup/start.sh

# Entry point
# At the start of container, tmp/vsts will be deleted, then created it for symbolic link
CMD mkdir /tmp/vsts && cp -a /backup/. /vsts/ && cd /vsts && ./start.sh 16.04