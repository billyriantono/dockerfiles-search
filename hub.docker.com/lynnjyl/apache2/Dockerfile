FROM ubuntu
MAINTAINER Yi-Ling Jia <lynnjyl@gmail.com>

RUN     apt-get update  && \
        apt-get install -y openssh-server apache2 supervisor    && \
        mkdir -p /var/run/sshd  && \
        mkdir -p /var/log/supervisor    && \
        apt-get remove -y --auto-remove curl make gcc   && \
        apt-get clean   && \
        rm -rf /var/lib/apt/lists/*


COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

EXPOSE 22 80
CMD ["/usr/bin/supervisord"]
