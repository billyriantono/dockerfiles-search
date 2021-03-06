#based on ekapusta/debian-sshd
FROM  debian:latest

EXPOSE 22
EXPOSE 17000-17999

ENV ROOT_PASSWORD dockerssh
ENV SSHD_CONFIG_PERMIT_ROOT_LOGIN yes
ENV SSHD_CONFIG_USE_PAM no
ENV SSHD_CONFIG_USE_DNS no

RUN \
    apt-get --quiet=2 update && \
    DEBIAN_FRONTEND=noninteractive \
        apt-get --assume-yes --no-install-recommends --quiet=2 install \
            p7zip-full curl apt-utils openssh-server mc && \
    apt-get clean && \
    rm --recursive --force /var/lib/apt/lists/* /tmp/* /var/tmp/*


WORKDIR /etc/ssh

RUN \
    echo "root:$ROOT_PASSWORD" | chpasswd && \
    echo "Root password changed" && \
    \
    sed --in-place 's/^\(PermitRootLogin\|UsePAM\|UseDNS\)/#\1/' sshd_config && \
    echo "" >> sshd_config && \
    echo "# Custom changes from `date`" >> sshd_config && \
    echo "PermitRootLogin $SSHD_CONFIG_PERMIT_ROOT_LOGIN" >> sshd_config && \
    echo "UsePAM $SSHD_CONFIG_USE_PAM" >> sshd_config && \
    echo "UseDNS $SSHD_CONFIG_USE_DNS" >> sshd_config && \
    echo "SSH daemon config updated"

# This will create all required directories/files
RUN service ssh start

CMD [ \
    # Path to OpenSSH SSH daemon
    "/usr/sbin/sshd", \
        # will not detach and does not become a daemon
        "-D", \
        # will send the output to the standard error instead of the system log
        "-e" \
]

WORKDIR /root
COPY shx.bash /root
RUN chmod +x /root/shx.bash

