FROM flocasts/alpine-jdk8:latest

# Install Sencha CMD
RUN curl -s -o /cmd.run.zip https://s3.amazonaws.com/sysadminconfs/sencha/SenchaCmd-6.7.0.63-linux-amd64.sh.zip && \
    unzip -p /cmd.run.zip > /cmd-install.run && \
    chmod +x /cmd-install.run && \
    /cmd-install.run -q -dir /opt/Sencha/Cmd/6.6.0.13 && \
    rm /cmd-install.run /cmd.run.zip

ENV PATH /opt/Sencha/Cmd/6.6.0.13:$PATH
