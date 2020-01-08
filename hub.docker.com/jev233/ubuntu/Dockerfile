FROM ubuntu:16.04

RUN echo '===*********===*********===********* setup.sh ===*********===*********===*********'

RUN mkdir -p /usr/share/biterika/provision
WORKDIR /usr/share/biterika/provision
COPY ./ /usr/share/biterika/provision
RUN chmod +x /usr/share/biterika/provision/setup.sh
RUN /usr/share/biterika/provision/setup.sh

RUN echo '===*********===*********===********* openssh ===*********===*********===*********'

RUN apt-get update && apt-get install -y openssh-server
RUN mkdir /var/run/sshd

RUN echo '===*********===*********===********* openssh set pass ===*********===*********===*********'
RUN echo 'root:barmalei911' | chpasswd
RUN echo '===*********===*********===********* openssh set pass END ===*********===*********===*********'
RUN sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config

# SSH login fix. Otherwise user is kicked off after login
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
