FROM ubuntu:trusty
MAINTAINER Howard Young <howard@zadarastorage.com>

RUN apt-get update && apt-get install -y openssh-server acl attr \
    ntp vim ntpdate winbind samba libnss-winbind libpam-winbind krb5-config krb5-locales krb5-user

RUN mkdir /var/run/sshd
RUN echo 'root:zadara' | chpasswd

RUN sed -i 's/PermitRootLogin without-password/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN echo 'UseDNS no' >> /etc/ssh/sshd_config

RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

ADD ./start.sh /start.sh

EXPOSE 22

CMD /start.sh
