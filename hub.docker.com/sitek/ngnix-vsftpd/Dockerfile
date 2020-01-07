FROM ubuntu

MAINTAINER Ramon Ontiveros, rontiveros@sitek.mx

RUN apt-get update && apt-get install -y nginx vsftpd openssh-server

# SSH login fix. Otherwise user is kicked off after login
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile
RUN echo "mkdir -p /var/run/sshd"
EXPOSE 21 22 80

COPY start.sh /usr/sbin/
RUN chmod +x /usr/sbin/start.sh

CMD ["/usr/sbin/start.sh"]