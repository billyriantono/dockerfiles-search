FROM codenvy/angular-yeoman

ADD package.json /tmp/application/package.json

RUN cd /tmp/application && \
    npm install && \
    cp -a /tmp/application/node_modules /home/user/application/

# 1. Use ADD instruction as root.
ADD . /tmp/app/
RUN cd /tmp/app && \
    cp -a /tmp/app/. /home/user/application/

