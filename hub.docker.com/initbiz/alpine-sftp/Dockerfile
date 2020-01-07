FROM alpine:latest

ENV USERNAMES="sftp"

RUN apk add --no-cache \
    openssh \
    && rm -rf /var/cache/apk/*

COPY root/ /

VOLUME /home

EXPOSE 22

RUN rm -rf /etc/ssh/ssh_host_rsa_key /etc/ssh/ssh_host_dsa_key && \ 
    ssh-keygen -f /etc/ssh/ssh_host_rsa_key -N '' -t rsa && \
    mkdir -p /var/run/sshd

CMD /bin/sh -c 'read -r -a array <<< "${USERNAMES}" && for element in "${array[@]}"; do addgroup -S $element && adduser -S $element -G $element done'

CMD ["/usr/sbin/sshd","-D"]