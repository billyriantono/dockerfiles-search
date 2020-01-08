FROM ubuntu:18.04

ENV DEBIAN_FRONTEND=noninteractive
RUN /usr/bin/apt-get update && /usr/bin/apt-get install -y apt-utils
RUN /usr/bin/apt-get install -y krb5-kdc krb5-admin-server krb5-user openssh-server

COPY krb5.conf /etc/krb5.conf
COPY kadm5.acl /etc/krb5kdc/kadm5.acl

RUN /usr/bin/touch /usr/local/bin/firstrun
COPY setup.sh /usr/local/bin/setup.sh
RUN /bin/chmod 0755 /usr/local/bin/setup.sh

RUN /bin/mkdir /run/sshd

EXPOSE 22 88 749

ENTRYPOINT [ "/usr/local/bin/setup.sh" ]
CMD [ "/usr/sbin/sshd", "-D" ]
