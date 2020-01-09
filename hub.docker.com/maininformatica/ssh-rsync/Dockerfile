FROM debian:testing
MAINTAINER Jose Tormo Main Informatica @maininformatica jtormo@main-informatica.com
#
#
# Paquetes
#
RUN apt-get update
RUN apt-get install --allow-unauthenticated -y supervisor make gcc libncurses5-dev bison flex mc joe git openssh-server rsync net-tools rsyslog
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/

# Ficheros Maestros
COPY ./sshd_config /etc/ssh/
COPY ./creausuario /usr/local/sbin/
COPY ./entrypoint.sh /etc/
RUN chmod a+x /usr/local/sbin/creausuario
RUN chmod a+x /etc/entrypoint.sh
RUN echo "/etc/entrypoint.sh" >> /root/.bashrc

# Preparamos SSH
RUN mkdir /var/run/sshd
RUN echo 'root:sshadmin' | chpasswd
COPY ./ssh_pam /etc/pam.d/sshd
EXPOSE 22

# Preparamos el RSYNC
RUN useradd rsync
COPY ./rsyncd.conf /etc/
RUN touch /etc/rsyncd.secretos
RUN chmod 600 /etc/rsyncd.secretos
EXPOSE 873

# Preparamos el Directorio Por defecto para Copias y grupo de CHROOT
RUN mkdir /backups
RUN mkdir /backups/rsync
RUN addgroup sftponly
RUN chmod 755 /backups/
RUN chown root:root /backups/
