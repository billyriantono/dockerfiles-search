FROM m9rco/alpine:3.5

ARG USER=root
ARG PASSWORD=root

RUN apk add -U --no-cache \
        openssh \
        bash \
        supervisor \
        git \
        zip \
        wget \
        curl \
    && sed -i s/#PermitRootLogin.*/PermitRootLogin\ yes/ /etc/ssh/sshd_config \
    && echo "${USER}:${PASSWORD}" | chpasswd \
    && ssh-keygen -A \
    && rm -rf /var/cache/apk/* 

ADD devfs /

SHELL ["/bin/bash","-ic"] 
RUN source ~/.bashrc

CMD ["supervisord", "--nodaemon", "--configuration", "/etc/supervisor/conf.d/supervisord.conf"]

EXPOSE 22
