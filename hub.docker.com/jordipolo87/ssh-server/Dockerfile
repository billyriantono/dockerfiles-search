FROM debian:jessie

ENV PASS 1234567890

RUN apt-get update
RUN apt-get -y install rsyslog
RUN apt-get install -y openssh-server
RUN apt-get install -y supervisor

RUN mkdir -p /var/run/sshd /var/log/supervisor

COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf
COPY initScript.sh /root/initScript.sh
RUN chmod 777 /root/initScript.sh

#==============================================
# SSH CONFIG COPIAT
RUN echo root:$PASS | chpasswd
RUN sed -i 's/PermitRootLogin without-password/PermitRootLogin yes/' /etc/ssh/sshd_config
# SSH login fix. Otherwise user is kicked off after login
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd
ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile
#===============================================

EXPOSE 22

CMD ["/usr/bin/supervisord"]

