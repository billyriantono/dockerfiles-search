FROM m9rco/go:1.10.8

ARG USER=root
ARG PASSWORD=root

RUN apk add -U --no-cache \
        godep \
        openssh \
        supervisor \
        autoconf \
        git \
        curl \
        wget \
        libc-dev \
        zip \
    # clean up       
    && rm -rf /var/cache/apk/* \
    # add ssh
    && sed -i s/#PermitRootLogin.*/PermitRootLogin\ yes/ /etc/ssh/sshd_config \
    && echo "${USER}:${PASSWORD}" | chpasswd \
    && ssh-keygen -A 

COPY devfs /

CMD ["/bin/bash", "-c", "env | grep GO >> /etc/environment && source ~/.bashrc && supervisord --nodaemon --configuration /etc/supervisor/conf.d/supervisord.conf"]

EXPOSE 22

