FROM andfilipe1/alpine-docker-node

MAINTAINER teste

#ENV APP_NAME app
#ENV APP_REPO bitbucket.org:REPO/app.git
ENV APP_PATH /app
ENV APP_JS app.js
ENV DEPLOY_KEY git-readonly.key
ENV NUM_PROCESSES 2
ENV MAX_MEMORY 250
ENV NODE_ENV production
ENV LISTEN_PORT 80 
ENV PORT 80

RUN mkdir -p ${APP_PATH} && \
    mkdir -p /root/.ssh && \
    echo "StrictHostKeyChecking=no" >> /root/.ssh/config && \
    echo "Host bitbucket.org" >> /root/.ssh/config && \
    echo "   HostName bitbucket.org" >> /root/.ssh/config && \
    echo "   IdentityFile /root/.ssh/${DEPLOY_KEY}" >> ~/.ssh/config && \
    echo "   User git" >> /root/.ssh/config && \
    echo "   Port 22" >> /root/.ssh/config

ADD ./${DEPLOY_KEY} /root/.ssh/
ADD ./pm2-start /usr/bin/

RUN apk add --no-cache curl git \
        openssh-client libgcc libstdc++ && \
    yarn global add bower pm2 http-server && \
    yarn cache clean && \
    rm -f /etc/localtime && \
    ln -s /usr/share/zoneinfo/America/Sao_Paulo /etc/localtime &&\
    rm -rf /usr/share/man /tmp/* /var/cache/apk/* /root/.npm /root/.yarn /root/.node-gyp /root/.gnupg \
        /usr/lib/node_modules/npm/man /usr/lib/node_modules/npm/doc /usr/lib/node_modules/npm/html && \
    chmod 0600 /root/.ssh/${DEPLOY_KEY} && \
    chmod +x /usr/bin/pm2-start

EXPOSE 80

WORKDIR $APP_PATH

CMD /usr/bin/pm2-start
