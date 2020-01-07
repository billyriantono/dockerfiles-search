FROM debian:stretch
RUN mkdir -p /var/run/sshd /var/log/supervisor
RUN echo 'root:password' | chpasswd
RUN apt-get update \
  && apt-get install -y openssh-server supervisor\
  && apt-get clean \
  && echo "Packages cleaned"
RUN sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf
EXPOSE 22
CMD ["/usr/bin/supervisord"]
