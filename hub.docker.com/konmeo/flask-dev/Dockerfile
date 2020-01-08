FROM konmeo/flask

USER root

RUN install_packages busybox curl tree htop git tig jq \
        openssh-client hdf5-tools sqlite3

ENV NODE_VERSION 8.10.0

RUN curl -sL "https://nodejs.org/dist/v$NODE_VERSION/node-v$NODE_VERSION-linux-x64.tar.gz" | \
        tar zxf - -C /usr/local --strip-components=1 --no-same-owner && \
    ln -s /usr/local/bin/node /usr/local/bin/nodejs

RUN bash -c "for i in \$(busybox | grep ,); do \
                 if [ -z \"\$(which \${i%,})\" ]; then \
                     ln -s /bin/busybox /bin/\${i%,}; \
                 fi; \
             done"
ENV EDITOR vi

ENV SHELL /bin/bash
