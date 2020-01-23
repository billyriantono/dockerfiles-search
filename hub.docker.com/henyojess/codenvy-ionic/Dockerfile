FROM henyojess/codenvy-cli
RUN sudo apt-get update && \
sudo apt-get install -y git=1:2.1.4-2.1 nodejs=0.10.29~dfsg-2 npm=1.4.21+ds-2 && \
sudo apt-get clean && \
sudo rm -rf /var/lib/apt/lists/* && \
sudo ln -sf /usr/bin/nodejs /usr/bin/node && \
sudo npm install -g ionic@1.5.0 cordova@5.0.0

EXPOSE 8100 35729
ENV CODENVY_APP_PORT_8100_HTTP 8100
ENV CODENVY_APP_BIND_DIR /home/user/runtime
VOLUME ["/home/user/runtime"]
CMD env | grep CODENVY_PORT | awk '{ print "export " $1 }' >> /home/user/.bashrc && sleep 4h
