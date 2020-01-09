FROM fstab/weechat-otr
MAINTAINER Fabian Stäber, fabian@fstab.de

USER root

RUN apt-get install -y \
    nodejs \
    npm

RUN ln -s /usr/bin/nodejs /usr/bin/node

ADD index.html /home/otr/index.html
ADD index.js /home/otr/index.js
ADD run-weechat.sh /home/otr/run-weechat.sh

USER otr

RUN npm install \
    express@3.4.4 \
    pty.js@0.2.4 \
    socket.io@0.9.16 \
    term.js@0.0.3

EXPOSE 8080

ENV SHELL /home/otr/run-weechat.sh

ENTRYPOINT echo "Starting server on http://`hostname -I | cut -d ' ' -f 1`:8080" && node index.js
