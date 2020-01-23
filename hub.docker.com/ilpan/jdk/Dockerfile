FROM openjdk:8-jdk-alpine3.8

LABEL maintainer=ilpan:<pna.dev@outlook.com>

ENV USERHOME /root

# add essential tools
RUN apk add --no-cache --update \
    openssh-server \
    openssh-client \
    bash \
    coreutils \
    procps

# configure ssh and shell
RUN \
    for t in rsa ecdsa ed25519; \
    do \
    ssh-keygen -t ${t} -P "" -f /etc/ssh/ssh_host_${t}_key; \
    done \
    ; \
    sed -ir "s/#PermitRootLogin.*/PermitRootLogin yes/" /etc/ssh/sshd_config \
    && sed -ir "s/.*StrictHostKeyChecking.*/StrictHostKeyChecking no/" /etc/ssh/ssh_config \
    && ssh-keygen -t rsa -P "" -f ${USERHOME}/.ssh/id_rsa \
    && cat ${USERHOME}/.ssh/id_rsa.pub >> /${USERHOME}/.ssh/authorized_keys \
    && echo "root:root" | chpasswd \
    && sed -ir "s#/root:/bin.*sh#/root:/bin/bash#g" /etc/passwd

WORKDIR ${USERHOME}

COPY ./docker-entrypoint.sh ./

EXPOSE 22

CMD [ "./docker-entrypoint.sh" ]