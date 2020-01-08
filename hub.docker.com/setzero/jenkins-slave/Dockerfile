FROM maven:3.5.4-jdk-8-alpine

ENV LANG=en_US.UTF-8 \
    TZ=Asia/Shanghai \
    ROOT_PASSWORD=root

RUN apk --no-cache add \
        openssh \
        supervisor \
        tzdata \
        git \
        docker \
        subversion \
    && sed -i s/#PermitRootLogin.*/PermitRootLogin\ yes/ /etc/ssh/sshd_config \
    && mkdir -p /var/logs/supervisor /var/run/supervisor \
    && rm -rf /var/cache/apk/* /tmp/* \
    && ssh-keygen -A

EXPOSE 22
CMD [ "/bin/sh","-c","cp /usr/share/zoneinfo/${TZ} /etc/localtime && \
                      echo ${TZ} > /etc/timezone && \
                      echo root:${ROOT_PASSWORD} | chpasswd && \
                      /usr/sbin/sshd -D" ]
