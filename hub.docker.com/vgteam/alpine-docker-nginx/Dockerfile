FROM vgteam/alpine-docker-base

MAINTAINER Victors Gold Devops Team

#ENV APP_NAME app
#ENV APP_REPO bitbucket.org:repo/${APP_NAME}.git
ENV APP_PATH /app
ENV DEPLOY_KEY git-readonly.key
#ENV NEWRELIC_LICENSE ""

RUN mkdir -p ${APP_PATH} && \
    mkdir -p /root/.ssh && \
    echo "StrictHostKeyChecking=no" >> /root/.ssh/config && \
    echo "Host bitbucket.org" >> /root/.ssh/config && \
    echo "   HostName bitbucket.org" >> /root/.ssh/config && \
    echo "   IdentityFile /root/.ssh/${DEPLOY_KEY}" >> ~/.ssh/config && \
    echo "   User git" >> /root/.ssh/config && \
    echo "   Port 22" >> /root/.ssh/config && \
    echo '@testing http://nl.alpinelinux.org/alpine/edge/testing' >> /etc/apk/repositories

ADD ./${DEPLOY_KEY} /root/.ssh/

RUN apk --update add --no-cache  \
        bash \
        git \
        curl \
        openssh \
        nginx && \
    update-ca-certificates && \
    chmod 0600 /root/.ssh/${DEPLOY_KEY} && \
    rm -rf /usr/share/man /tmp/* /var/cache/apk/* && \
    rm -f /etc/localtime && \
    ln -s /usr/share/zoneinfo/America/Sao_Paulo /etc/localtime

# Copy custom configuration file from the current directory
COPY conf.d/*.conf /etc/nginx/conf.d/
COPY nginx.conf /etc/nginx/

RUN sed -i "s#__APP_PATH__#$APP_PATH#g" /etc/nginx/conf.d/default.conf && \
    sed -i "s#__APP_PATH__#$APP_PATH#g" /etc/nginx/nginx.conf && \
    chown nginx: -R /var/lib/nginx

# Define working directory
WORKDIR $APP_PATH

RUN ln -sf /dev/stdout /var/log/nginx/access.log
RUN ln -sf /dev/stderr /var/log/nginx/error.log

EXPOSE 80

CMD ["sh", "-c", "nginx -g 'daemon off;'"]
