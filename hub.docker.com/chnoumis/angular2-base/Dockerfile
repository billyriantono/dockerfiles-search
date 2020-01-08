FROM chnoumis/node

USER root
RUN apk add --update sudo
RUN cp /etc/sudoers /etc/sudoers.bk
RUN echo 'chnoumis ALL=(ALL:ALL) NOPASSWD: ALL' >> /etc/sudoers
# Bundle app source
COPY . /opt/chnoumis/node/app
RUN chown -R chnoumis:chnoumis /opt/chnoumis/node 
USER chnoumis

# Add private repo
# ADD npmrc /home/chnoumis/.npmrc
# ADD npmrc /root/.npmrc
 
RUN cd /opt/chnoumis/node/app && npm install
# RUN cp -a /opt/chnoumis/node/build/node_modules /opt/chnoumis/node/app 
# RUN rm -r /opt/chnoumis/node/build/*
RUN cd /opt/chnoumis/node/app && ls | grep -v 'node_modules' | xargs rm -rf

# Removed due to EXDEV: cross-device link not permitted
RUN rm -rf /opt/chnoumis/node/app/node_modules/boxen 
RUN rm -rf /opt/chnoumis/node/app/node_modules/popsicle-proxy-agent 
RUN rm -rf /opt/chnoumis/node/app/node_modules/popsicle-retry 
RUN rm -rf /opt/chnoumis/node/app/node_modules/popsicle-status 
RUN rm -rf /opt/chnoumis/node/app/node_modules/popsicle
RUN rm -rf /opt/chnoumis/node/app/node_modules/typings-core
RUN rm -rf /opt/chnoumis/node/app/node_modules/update-notifier
RUN rm -rf /opt/chnoumis/node/app/node_modules/typings
RUN rm -rf /opt/chnoumis/node/app/node_modules/@ngrx/store
RUN rm -rf /opt/chnoumis/node/app/node_modules/yargs
RUN rm -rf /opt/chnoumis/node/app/node_modules/browser-sync
RUN rm -rf /opt/chnoumis/node/app/node_modules/systemjs


USER root
RUN rm /etc/sudoers
RUN mv /etc/sudoers.bk /etc/sudoers
RUN chown -R chnoumis:chnoumis /opt/chnoumis/node
USER chnoumis
